---
title: 'Esercitazione: integrazione di Azure Active Directory con Confluence SAML SSO by Microsoft | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Confluence SAML SSO by Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 56de86df9c915fa7c41e3bf0a545cc528cdcf959
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="a4394-103">Esercitazione: Integrazione di Azure Active Directory con Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="a4394-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="a4394-104">Questa esercitazione descrive come integrare Confluence SAML SSO by Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4394-104">In this tutorial, you learn how to integrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4394-105">L'integrazione di Confluence SAML SSO by Microsoft con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a4394-106">È possibile controllare in Azure AD chi ha accesso a Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="a4394-106">You can control in Azure AD who has access to Confluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="a4394-107">È possibile abilitare gli utenti per l'accesso automatico a Confluence SAML SSO by Microsoft, ovvero per il Single Sign-On, con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-107">You can enable your users to automatically get signed-on to Confluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4394-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4394-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a4394-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4394-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4394-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4394-110">Prerequisites</span></span>

<span data-ttu-id="a4394-111">Per configurare l'integrazione di Azure AD con Confluence SAML SSO by Microsoft sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-111">To configure Azure AD integration with Confluence SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="a4394-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4394-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4394-113">Applicazione server Confluence installata in un server di Windows a 64 bit (in locale o nell'infrastruttura IaaS cloud)</span><span class="sxs-lookup"><span data-stu-id="a4394-113">Confluence server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="a4394-114">Server Confluence abilitato per HTTPS</span><span class="sxs-lookup"><span data-stu-id="a4394-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="a4394-115">Si noti che le versioni supportate per il plug-in Confluence sono indicate nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="a4394-115">Note the supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="a4394-116">Il server Confluence deve essere raggiungibile da Internet, in particolare per la pagina di accesso di Azure AD per l'autenticazione e deve essere in grado di ricevere il token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-116">Confluence server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="a4394-117">Credenziali di amministratore configurate in Confluence</span><span class="sxs-lookup"><span data-stu-id="a4394-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="a4394-118">WebSudo disabilitato in Confluence</span><span class="sxs-lookup"><span data-stu-id="a4394-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="a4394-119">Utente di test creato nell'applicazione server Confluence</span><span class="sxs-lookup"><span data-stu-id="a4394-119">Test user created in the Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="a4394-120">Non è consigliabile usare un ambiente di produzione di Confluence per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4394-120">To test the steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="a4394-121">Testare prima di tutto l'integrazione nell'ambiente di sviluppo o di gestione temporanea dell'applicazione e poi usare l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a4394-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="a4394-122">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4394-123">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a4394-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4394-124">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4394-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="a4394-125">Versioni di Confluence supportate</span><span class="sxs-lookup"><span data-stu-id="a4394-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="a4394-126">A tutt'oggi sono supportate le versioni seguenti di Confluence:</span><span class="sxs-lookup"><span data-stu-id="a4394-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="a4394-127">Confluence: da 5.0 a 5.10</span><span class="sxs-lookup"><span data-stu-id="a4394-127">Confluence: 5.0 to 5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4394-128">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a4394-128">Scenario description</span></span>
<span data-ttu-id="a4394-129">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a4394-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4394-130">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-130">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4394-131">Aggiunta di Confluence SAML SSO by Microsoft dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4394-131">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="a4394-132">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="a4394-133">Aggiunta di Confluence SAML SSO by Microsoft dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4394-133">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="a4394-134">Per configurare l'integrazione di Confluence SAML SSO by Microsoft in Azure AD è necessario aggiungere Confluence SAML SSO by Microsoft dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a4394-134">To configure the integration of Confluence SAML SSO by Microsoft into Azure AD, you need to add Confluence SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a4394-135">**Per aggiungere Confluence SAML SSO by Microsoft dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4394-135">**To add Confluence SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a4394-136">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4394-136">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4394-138">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a4394-138">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a4394-139">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4394-139">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a4394-141">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4394-141">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a4394-143">Nella casella di ricerca digitare **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a4394-143">In the search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="a4394-145">Nel riquadro dei risultati selezionare **Confluence SAML SSO by Microsoft** e quindi fare clic su **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4394-145">In the results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4394-147">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4394-148">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Confluence SAML SSO by Microsoft mediante un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a4394-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4394-149">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Confluence SAML SSO by Microsoft corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4394-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Confluence SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="a4394-150">In altre parole è necessario stabilire una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-150">In other words, a link relationship between an Azure AD user and the related user in Confluence SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="a4394-151">Per stabilire la relazione di collegamento, in Confluence SAML SSO by Microsoft assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="a4394-151">In Confluence SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a4394-152">Per configurare e testare l'accesso Single Sign-On di Azure AD con Confluence SAML SSO by Microsoft è necessario completare le operazioni di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-152">To configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4394-153">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4394-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4394-154">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4394-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4394-155">**[Creazione di un utente di test di Confluence SAML SSO by Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**: per avere una controparte di Britta Simon in Confluence SAML SSO by Microsoft collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4394-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4394-156">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4394-156">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4394-157">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a4394-157">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4394-158">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4394-159">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-159">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="a4394-160">**Per configurare l'accesso Single Sign-On di Azure AD con Confluence SAML SSO by Microsoft, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4394-160">**To configure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="a4394-161">Nella pagina di integrazione dell'applicazione **Confluence SAML SSO by Microsoft** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4394-161">In the Azure portal, on the **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a4394-163">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a4394-163">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="a4394-165">Nella sezione **URL e dominio Confluence SAML SSO by Microsoft** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4394-165">On the **Confluence SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="a4394-167">a.</span><span class="sxs-lookup"><span data-stu-id="a4394-167">a.</span></span> <span data-ttu-id="a4394-168">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<domain:port>/plugins/servlet/saml/auth`.</span><span class="sxs-lookup"><span data-stu-id="a4394-168">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="a4394-169">b.</span><span class="sxs-lookup"><span data-stu-id="a4394-169">b.</span></span> <span data-ttu-id="a4394-170">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="a4394-170">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="a4394-171">c.</span><span class="sxs-lookup"><span data-stu-id="a4394-171">c.</span></span> <span data-ttu-id="a4394-172">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="a4394-172">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a4394-173">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="a4394-173">These values are not real.</span></span> <span data-ttu-id="a4394-174">aggiornarli con l'identificatore, l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="a4394-174">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a4394-175">La porta è facoltativa nel caso di un URL denominato.</span><span class="sxs-lookup"><span data-stu-id="a4394-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="a4394-176">Questi valori vengono ricevuti durante la configurazione del plug-in Confluence, illustrata più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4394-176">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>
 

4. <span data-ttu-id="a4394-177">Per generare l'URL dei **metadati**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4394-177">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="a4394-178">a.</span><span class="sxs-lookup"><span data-stu-id="a4394-178">a.</span></span> <span data-ttu-id="a4394-179">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="a4394-179">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="a4394-181">b.</span><span class="sxs-lookup"><span data-stu-id="a4394-181">b.</span></span> <span data-ttu-id="a4394-182">Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="a4394-182">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="a4394-184">c.</span><span class="sxs-lookup"><span data-stu-id="a4394-184">c.</span></span> <span data-ttu-id="a4394-185">Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="a4394-185">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="a4394-187">d.</span><span class="sxs-lookup"><span data-stu-id="a4394-187">d.</span></span> <span data-ttu-id="a4394-188">Passare ora alla pagina delle proprietà di **Confluence SAML SSO by Microsoft**, copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="a4394-188">Now go to the property page of **Confluence SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="a4394-190">e.</span><span class="sxs-lookup"><span data-stu-id="a4394-190">e.</span></span> <span data-ttu-id="a4394-191">Generare l'**URL dei metadati** usando il modello seguente `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copiare il valore nel Blocco note, perché verrà usato in seguito per la configurazione del plug-in.</span><span class="sxs-lookup"><span data-stu-id="a4394-191">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="a4394-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a4394-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a4394-194">Contattare [Microsoft](mailto:waadpartners@microsoft.com) con le informazioni seguenti per il plug-in Confluence.</span><span class="sxs-lookup"><span data-stu-id="a4394-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the Confluence plugin.</span></span>
    
    *   <span data-ttu-id="a4394-195">Nome del cliente:</span><span class="sxs-lookup"><span data-stu-id="a4394-195">Customer Name:</span></span>
    *   <span data-ttu-id="a4394-196">Nome del dominio primario:</span><span class="sxs-lookup"><span data-stu-id="a4394-196">Primary domain name:</span></span>
    *   <span data-ttu-id="a4394-197">Azure AD Premium: sì/no. Il plug-in è disponibile per tutte le SKU per i clienti, ovvero livello Gratuito, Base e Premium</span><span class="sxs-lookup"><span data-stu-id="a4394-197">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="a4394-198">Numero di utenti che useranno questa integrazione:</span><span class="sxs-lookup"><span data-stu-id="a4394-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="a4394-199">Versione Confluence:</span><span class="sxs-lookup"><span data-stu-id="a4394-199">Confluence Version:</span></span>
    *   <span data-ttu-id="a4394-200">Commenti:</span><span class="sxs-lookup"><span data-stu-id="a4394-200">Comments:</span></span>

7. <span data-ttu-id="a4394-201">In un'altra finestra del Web browser accedere all'istanza di Confluence come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4394-201">In a different web browser window, log in to your Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="a4394-202">Passare il puntatore del mouse sulla rotellina e scegliere **Add-ons** (Componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="a4394-202">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="a4394-204">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Manage add-ons** (Gestisci componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="a4394-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="a4394-206">Caricare manualmente il plug-in offerto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-206">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="a4394-207">Dopo aver installato il plug-in, questo comparirà nella sezione dei componenti aggiuntivi **User Installed** (Installati dall'utente) della sezione **Manage Add-on** (Gestisci componente aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="a4394-207">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="a4394-208">Fare clic su **Configure** (Configura) per configurare il nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="a4394-208">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="a4394-209">Seguire questa procedura nella pagina di configurazione:</span><span class="sxs-lookup"><span data-stu-id="a4394-209">Perform following steps on configuration page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="a4394-211">a.</span><span class="sxs-lookup"><span data-stu-id="a4394-211">a.</span></span> <span data-ttu-id="a4394-212">In **Metadata URL** (URL metadati) incollare l'**URL dei metadati** generato da Azure AD e fare clic sul pulsante **Resolve** (Risolvi).</span><span class="sxs-lookup"><span data-stu-id="a4394-212">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="a4394-213">Viene letto l'URL dei metadati IdP e vengono compilate tutte le informazioni dei campi.</span><span class="sxs-lookup"><span data-stu-id="a4394-213">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="a4394-214">La posizione predefinita dell'ID utente SAML è nell'identificatore del nome.</span><span class="sxs-lookup"><span data-stu-id="a4394-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="a4394-215">È possibile sostituirlo con un attributo e immettere il nome dell'attributo appropriato.</span><span class="sxs-lookup"><span data-stu-id="a4394-215">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="a4394-216">Assicurarsi che esista un solo certificato mappato per l'app in modo che non si verifichino errori durante la risoluzione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="a4394-216">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="a4394-217">Se sono presenti più certificati, durante la risoluzione dei metadati, l'amministratore riceve un errore.</span><span class="sxs-lookup"><span data-stu-id="a4394-217">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="a4394-218">b.</span><span class="sxs-lookup"><span data-stu-id="a4394-218">b.</span></span> <span data-ttu-id="a4394-219">Copiare i valori di **identificatore, URL di risposta e URL di accesso** e incollarli rispettivamente nelle caselle **Identificatore, URL di risposta e URL di accesso** nella sezione **Dominio e URL Confluence SAML SSO by Microsoft** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4394-219">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="a4394-220">c.</span><span class="sxs-lookup"><span data-stu-id="a4394-220">c.</span></span> <span data-ttu-id="a4394-221">In **Login Button Name** (Nome pulsante di accesso) digitare il nome del pulsante che l'organizzazione vuole mostrare agli utenti nella schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4394-221">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="a4394-222">d.</span><span class="sxs-lookup"><span data-stu-id="a4394-222">d.</span></span> <span data-ttu-id="a4394-223">In **SAML User ID Locations** (Posizioni ID utente SAML) selezionare **User ID is in the NameIdentifier element of the Subject statement** (ID utente nell'elemento NameIdentifier dell'istruzione Subject) oppure **User ID is in an Attribute element** (ID utente in un elemento Attribute).</span><span class="sxs-lookup"><span data-stu-id="a4394-223">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="a4394-224">Questo ID deve essere l'ID utente di Confluence.</span><span class="sxs-lookup"><span data-stu-id="a4394-224">This ID has to be the Confluence user id.</span></span> <span data-ttu-id="a4394-225">Se non viene trovata una corrispondenza per l'ID utente, il sistema non consentirà agli utenti di accedere.</span><span class="sxs-lookup"><span data-stu-id="a4394-225">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="a4394-226">e.</span><span class="sxs-lookup"><span data-stu-id="a4394-226">e.</span></span> <span data-ttu-id="a4394-227">Se si seleziona l'opzione **User ID is in an Attribute element** (ID utente in un elemento Attribute), nella casella di testo **Attribute name** (Nome attributo) digitare il nome dell'attributo per cui è previsto l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="a4394-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="a4394-228">f.</span><span class="sxs-lookup"><span data-stu-id="a4394-228">f.</span></span> <span data-ttu-id="a4394-229">Se si usa un dominio federato, come AD FS o altri, con Azure AD fare clic sull'opzione **Enable Home Realm Discovery** (Abilita individuazione area di autenticazione principale) e configurare **Domain Name** (Nome dominio).</span><span class="sxs-lookup"><span data-stu-id="a4394-229">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="a4394-230">g.</span><span class="sxs-lookup"><span data-stu-id="a4394-230">g.</span></span> <span data-ttu-id="a4394-231">In **Domain Name** (Nome dominio) digitare il nome del dominio in caso di accesso basato su AD FS.</span><span class="sxs-lookup"><span data-stu-id="a4394-231">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="a4394-232">h.</span><span class="sxs-lookup"><span data-stu-id="a4394-232">h.</span></span> <span data-ttu-id="a4394-233">Selezionare **Enable Single Sign out** (Abilita Single Sign-Out) per impostare la disconnessione da Azure AD quando un utente si disconnette da Confluence.</span><span class="sxs-lookup"><span data-stu-id="a4394-233">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="a4394-234">i.</span><span class="sxs-lookup"><span data-stu-id="a4394-234">i.</span></span> <span data-ttu-id="a4394-235">Fare clic sul pulsante **Save** (Salva) per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a4394-235">Click **Save** button to save the settings.</span></span>


> [!TIP]
> <span data-ttu-id="a4394-236">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a4394-236">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a4394-237">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a4394-237">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a4394-238">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4394-238">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4394-239">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4394-240">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4394-240">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a4394-242">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4394-242">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4394-243">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4394-243">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4394-245">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a4394-245">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4394-247">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a4394-247">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4394-249">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4394-249">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4394-251">a.</span><span class="sxs-lookup"><span data-stu-id="a4394-251">a.</span></span> <span data-ttu-id="a4394-252">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4394-252">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4394-253">b.</span><span class="sxs-lookup"><span data-stu-id="a4394-253">b.</span></span> <span data-ttu-id="a4394-254">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4394-254">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4394-255">c.</span><span class="sxs-lookup"><span data-stu-id="a4394-255">c.</span></span> <span data-ttu-id="a4394-256">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a4394-256">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a4394-257">d.</span><span class="sxs-lookup"><span data-stu-id="a4394-257">d.</span></span> <span data-ttu-id="a4394-258">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a4394-258">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="a4394-259">Creazione di un utente di test di Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="a4394-259">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="a4394-260">Per consentire agli utenti di Azure AD di accedere a un server Confluence locale, è necessario effettuarne il provisioning in Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-260">To enable Azure AD users to log in to Confluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="a4394-261">In Confluence SAML SSO by Microsoft il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a4394-261">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="a4394-262">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4394-262">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a4394-263">Accedere al server locale Confluence come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4394-263">Log in to your Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="a4394-264">Passare il puntatore del mouse e fare clic su **User management** (Gestione utenti).</span><span class="sxs-lookup"><span data-stu-id="a4394-264">Hover on cog and click the **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="a4394-266">Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti).</span><span class="sxs-lookup"><span data-stu-id="a4394-266">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="a4394-267">Nella pagina della finestra di dialogo **"Add a User"** (Aggiungi un utente) eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a4394-267">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="a4394-269">a.</span><span class="sxs-lookup"><span data-stu-id="a4394-269">a.</span></span> <span data-ttu-id="a4394-270">Nella casella di testo **Username** (Nome utente) digitare l'indirizzo di posta elettronica di un utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4394-270">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="a4394-271">b.</span><span class="sxs-lookup"><span data-stu-id="a4394-271">b.</span></span> <span data-ttu-id="a4394-272">Nella casella di testo **Full Name** (Nome completo) digitare il nome completo dell'utente, ad esempio Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4394-272">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="a4394-273">c.</span><span class="sxs-lookup"><span data-stu-id="a4394-273">c.</span></span> <span data-ttu-id="a4394-274">Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a4394-274">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a4394-275">d.</span><span class="sxs-lookup"><span data-stu-id="a4394-275">d.</span></span> <span data-ttu-id="a4394-276">Nella casella di testo **Password** digitare la password di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4394-276">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="a4394-277">e.</span><span class="sxs-lookup"><span data-stu-id="a4394-277">e.</span></span> <span data-ttu-id="a4394-278">Fare clic sul pulsante **Confirm** (Conferma) e immettere di nuovo la password.</span><span class="sxs-lookup"><span data-stu-id="a4394-278">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="a4394-279">f.</span><span class="sxs-lookup"><span data-stu-id="a4394-279">f.</span></span> <span data-ttu-id="a4394-280">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a4394-280">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a4394-281">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4394-281">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a4394-282">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure AD concedendole l'accesso a Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-282">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Confluence SAML SSO by Microsoft.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a4394-284">**Per assegnare Britta Simon a Confluence SAML SSO by Microsoft, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4394-284">**To assign Britta Simon to Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="a4394-285">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a4394-285">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a4394-287">Nell'elenco delle applicazioni selezionare **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a4394-287">In the applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="a4394-289">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a4394-289">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a4394-291">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a4394-291">Click **Add** button.</span></span> <span data-ttu-id="a4394-292">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a4394-292">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a4394-294">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a4394-294">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a4394-295">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a4394-295">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4394-296">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a4394-296">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4394-297">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4394-297">Testing single sign-on</span></span>

<span data-ttu-id="a4394-298">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4394-298">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a4394-299">Quando si fa clic sul riquadro Confluence SAML SSO by Microsoft nel pannello di accesso si accede automaticamente all'applicazione Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4394-299">When you click the Confluence SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="a4394-300">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4394-300">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4394-301">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a4394-301">Additional resources</span></span>

* [<span data-ttu-id="a4394-302">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4394-302">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4394-303">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4394-303">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

