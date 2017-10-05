---
title: 'Esercitazione: Integrazione di Azure Active Directory con Ceridian Dayforce HCM | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Ceridian Dayforce HCM.
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
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="c4923-103">Esercitazione: Integrazione di Azure Active Directory con Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="c4923-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="c4923-104">Questa esercitazione descrive come integrare Ceridian Dayforce HCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4923-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4923-105">L'integrazione di Ceridian Dayforce HCM con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4923-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4923-106">È possibile controllare in Azure AD chi può accedere a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="c4923-107">È possibile abilitare gli utenti per l'accesso automatico a Ceridian Dayforce HCM (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4923-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c4923-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4923-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c4923-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4923-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4923-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c4923-110">Prerequisites</span></span>

<span data-ttu-id="c4923-111">Per configurare l'integrazione di Azure AD con Ceridian Dayforce HCM, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4923-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="c4923-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4923-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4923-113">Sottoscrizione di Ceridian Dayforce HCM abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c4923-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4923-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4923-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4923-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4923-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c4923-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4923-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4923-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4923-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c4923-118">Scenario description</span></span>
<span data-ttu-id="c4923-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c4923-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4923-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4923-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4923-121">Aggiunta di Ceridian Dayforce HCM dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c4923-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="c4923-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="c4923-123">Aggiunta di Ceridian Dayforce HCM dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c4923-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="c4923-124">Per configurare l'integrazione di Ceridian Dayforce HCM in Azure AD, è necessario aggiungere Ceridian Dayforce HCM dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c4923-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4923-125">**Per aggiungere Ceridian Dayforce HCM dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4923-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4923-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c4923-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="c4923-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c4923-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4923-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c4923-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="c4923-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="c4923-133">Nella casella di ricerca, digitare **Ceridian Dayforce HCM**, selezionare **Ceridian Dayforce HCM** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM nell'elenco risultati](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c4923-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c4923-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Ceridian Dayforce HCM usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c4923-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4923-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Ceridian Dayforce HCM corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4923-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="c4923-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="c4923-139">Per stabilire la relazione di collegamento, in Ceridian Dayforce HCM assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c4923-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c4923-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Ceridian Dayforce HCM, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4923-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4923-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c4923-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4923-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4923-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4923-143">**[Creare un utente di test di Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**: per avere una controparte di Britta Simon in Ceridian Dayforce HCM collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4923-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4923-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4923-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4923-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c4923-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c4923-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c4923-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="c4923-148">**Per configurare Single Sign-On di Azure AD con Ceridian Dayforce HCM, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4923-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="c4923-149">Nella pagina di integrazione dell'applicazione **Ceridian Dayforce HCM** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c4923-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="c4923-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c4923-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="c4923-153">Nella sezione **URL e dominio Ceridian Dayforce HCM** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4923-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="c4923-155">a.</span><span class="sxs-lookup"><span data-stu-id="c4923-155">a.</span></span> <span data-ttu-id="c4923-156">Nella casella di testo **URL di accesso** , digitare l'URL utilizzato dagli utenti per accedere all'applicazione Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="c4923-157">Environment</span><span class="sxs-lookup"><span data-stu-id="c4923-157">Environment</span></span> | <span data-ttu-id="c4923-158">URL</span><span class="sxs-lookup"><span data-stu-id="c4923-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="c4923-159">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="c4923-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="c4923-160">Per il test</span><span class="sxs-lookup"><span data-stu-id="c4923-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="c4923-161">b.</span><span class="sxs-lookup"><span data-stu-id="c4923-161">b.</span></span> <span data-ttu-id="c4923-162">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4923-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="c4923-163">Environment</span><span class="sxs-lookup"><span data-stu-id="c4923-163">Environment</span></span> | <span data-ttu-id="c4923-164">URL</span><span class="sxs-lookup"><span data-stu-id="c4923-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="c4923-165">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="c4923-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="c4923-166">Per il test</span><span class="sxs-lookup"><span data-stu-id="c4923-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="c4923-167">c.</span><span class="sxs-lookup"><span data-stu-id="c4923-167">c.</span></span> <span data-ttu-id="c4923-168">Nella casella di testo **URL di risposta** digitare l'URL utilizzato da Azure AD per inserire la risposta.</span><span class="sxs-lookup"><span data-stu-id="c4923-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="c4923-169">Environment</span><span class="sxs-lookup"><span data-stu-id="c4923-169">Environment</span></span> | <span data-ttu-id="c4923-170">URL</span><span class="sxs-lookup"><span data-stu-id="c4923-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="c4923-171">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="c4923-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="c4923-172">Per il test</span><span class="sxs-lookup"><span data-stu-id="c4923-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="c4923-173">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="c4923-173">These values are not real.</span></span> <span data-ttu-id="c4923-174">è necessario aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c4923-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="c4923-175">Per ottenere questi valori, contattare il [team di supporto clienti di Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="c4923-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="c4923-176">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c4923-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="c4923-178">L'applicazione Ceridian Dayforce HCM si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="c4923-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c4923-179">Collaborare con il [team di supporto di Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) per individuare l'identificatore utente corretto.</span><span class="sxs-lookup"><span data-stu-id="c4923-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="c4923-180">Microsoft consiglia di utilizzare l'attributo **"name"** come identificatore utente.</span><span class="sxs-lookup"><span data-stu-id="c4923-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="c4923-181">È possibile gestire i valori di questi attributi dalla sezione **Attributi utente** nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="c4923-182">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-182">The following screenshot shows an example for this.</span></span>  

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="c4923-184">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4923-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c4923-185">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="c4923-185">Attribute Name</span></span>  | <span data-ttu-id="c4923-186">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="c4923-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="c4923-187">name</span><span class="sxs-lookup"><span data-stu-id="c4923-187">name</span></span>  | <span data-ttu-id="c4923-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="c4923-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="c4923-189">a.</span><span class="sxs-lookup"><span data-stu-id="c4923-189">a.</span></span> <span data-ttu-id="c4923-190">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="c4923-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c4923-193">b.</span><span class="sxs-lookup"><span data-stu-id="c4923-193">b.</span></span> <span data-ttu-id="c4923-194">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="c4923-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c4923-195">c.</span><span class="sxs-lookup"><span data-stu-id="c4923-195">c.</span></span> <span data-ttu-id="c4923-196">Nell'elenco **Valore** selezionare l'attributo utente da usare per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="c4923-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="c4923-197">Ad esempio, se si vuole usare il valore EmployeeID come identificatore utente univoco e il valore dell'attributo è stato archiviato in ExtensionAttribute2, selezionare **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="c4923-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="c4923-198">d.</span><span class="sxs-lookup"><span data-stu-id="c4923-198">d.</span></span> <span data-ttu-id="c4923-199">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4923-199">Click **Ok**.</span></span>

7. <span data-ttu-id="c4923-200">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c4923-200">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="c4923-202">Nella sezione **Configurazione di Ceridian Dayforce HCM** fare clic su **Configura Ceridian Dayforce HCM** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c4923-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c4923-203">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c4923-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="c4923-205">Per configurare l'accesso Single Sign-On sul lato **Ceridian Dayforce HCM**, è necessario inviare il file **XML metadati** scaricato, l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** al [team di supporto di Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="c4923-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="c4923-206">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4923-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4923-207">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c4923-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4923-208">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4923-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c4923-209">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-209">Create an Azure AD test user</span></span>

<span data-ttu-id="c4923-210">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4923-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="c4923-212">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c4923-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4923-213">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="c4923-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c4923-215">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c4923-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c4923-217">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c4923-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c4923-219">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c4923-219">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c4923-221">a.</span><span class="sxs-lookup"><span data-stu-id="c4923-221">a.</span></span> <span data-ttu-id="c4923-222">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4923-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4923-223">b.</span><span class="sxs-lookup"><span data-stu-id="c4923-223">b.</span></span> <span data-ttu-id="c4923-224">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4923-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c4923-225">c.</span><span class="sxs-lookup"><span data-stu-id="c4923-225">c.</span></span> <span data-ttu-id="c4923-226">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="c4923-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c4923-227">d.</span><span class="sxs-lookup"><span data-stu-id="c4923-227">d.</span></span> <span data-ttu-id="c4923-228">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c4923-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="c4923-229">Creazione di un utente di test Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="c4923-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="c4923-230">Questa sezione descrive come creare un utente chiamato Britta Simon in Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="c4923-231">Collaborare con il [team di supporto di Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) per aggiungere gli utenti all'applicazione Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4923-232">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4923-233">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c4923-235">**Per assegnare Britta Simon a Ceridian Dayforce HCM, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4923-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="c4923-236">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c4923-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c4923-238">Nell'elenco delle applicazioni, selezionare **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="c4923-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="c4923-240">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c4923-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c4923-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c4923-242">Click **Add** button.</span></span> <span data-ttu-id="c4923-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4923-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c4923-245">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c4923-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4923-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c4923-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4923-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4923-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c4923-248">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4923-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="c4923-249">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="c4923-251">**Per assegnare Britta Simon a Ceridian Dayforce HCM, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c4923-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="c4923-252">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c4923-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c4923-254">Nell'elenco delle applicazioni, selezionare **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="c4923-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Il collegamento Ceridian Dayforce HCM nell'elenco delle applicazioni](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="c4923-256">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c4923-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="c4923-258">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c4923-258">Click **Add** button.</span></span> <span data-ttu-id="c4923-259">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4923-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="c4923-261">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c4923-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4923-262">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c4923-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4923-263">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c4923-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c4923-264">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c4923-264">Test single sign-on</span></span>

<span data-ttu-id="c4923-265">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c4923-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="c4923-266">Quando si fa clic sul riquadro Ceridian Dayforce HCM nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="c4923-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4923-267">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c4923-267">Additional resources</span></span>

* [<span data-ttu-id="c4923-268">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4923-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4923-269">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4923-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

