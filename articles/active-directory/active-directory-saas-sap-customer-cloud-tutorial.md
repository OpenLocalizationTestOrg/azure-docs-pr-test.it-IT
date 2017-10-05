---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAP Cloud for Customer.
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
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="7fb01-103">Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="7fb01-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="7fb01-104">Questa esercitazione descrive come integrare SAP Cloud for Customer con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fb01-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fb01-105">L'integrazione di SAP Cloud for Customer con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7fb01-106">È possibile controllare in Azure AD chi può accedere a SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="7fb01-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="7fb01-107">È possibile abilitare gli utenti per l'accesso automatico a SAP Cloud for Customer (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fb01-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb01-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7fb01-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fb01-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fb01-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7fb01-110">Prerequisites</span></span>

<span data-ttu-id="7fb01-111">Per configurare l'integrazione di Azure AD con SAP Cloud for Customer, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="7fb01-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fb01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fb01-113">Sottoscrizione di SAP Cloud for Customer abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7fb01-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fb01-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7fb01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fb01-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fb01-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7fb01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fb01-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fb01-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fb01-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7fb01-118">Scenario description</span></span>
<span data-ttu-id="7fb01-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7fb01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fb01-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fb01-121">Aggiunta di SAP Cloud for Customer dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7fb01-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="7fb01-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="7fb01-123">Aggiunta di SAP Cloud for Customer dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7fb01-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="7fb01-124">Per configurare l'integrazione di SAP Cloud for Customer in Azure AD, è necessario aggiungere SAP Cloud for Customer dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7fb01-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7fb01-125">**Per aggiungere SAP Cloud for Customer dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7fb01-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb01-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7fb01-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fb01-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7fb01-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7fb01-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="7fb01-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7fb01-133">Nella casella di ricerca, digitare **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="7fb01-135">Nel riquadro dei risultati selezionare **SAP Cloud for Customer** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7fb01-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fb01-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fb01-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Cloud for Customer con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7fb01-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fb01-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SAP Cloud for Customer che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fb01-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="7fb01-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="7fb01-141">Per stabilire la relazione di collegamento, in SAP Cloud for Customer assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7fb01-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SAP Cloud for Customer, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7fb01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7fb01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7fb01-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7fb01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fb01-145">**[Creazione di un utente di test di SAP Cloud for Customer](#creating-a-sap-cloud-for-customer-test-user)**: per avere una controparte di Britta Simon in SAP Cloud for Customer collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fb01-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fb01-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fb01-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fb01-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7fb01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fb01-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fb01-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="7fb01-150">**Per configurare l'accesso Single Sign-On di Azure AD con SAP Cloud for Customer, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7fb01-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb01-151">Nella pagina di integrazione dell'applicazione **SAP Cloud for Customer** del portale di Azure, fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7fb01-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7fb01-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="7fb01-155">Nella sezione **URL e dominio SAP Cloud for Customer** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7fb01-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="7fb01-157">a.</span><span class="sxs-lookup"><span data-stu-id="7fb01-157">a.</span></span> <span data-ttu-id="7fb01-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server name>.crm.ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="7fb01-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="7fb01-159">b.</span><span class="sxs-lookup"><span data-stu-id="7fb01-159">b.</span></span> <span data-ttu-id="7fb01-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="7fb01-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fb01-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="7fb01-161">These values are not real.</span></span> <span data-ttu-id="7fb01-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="7fb01-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7fb01-163">Per ottenere questi valori, contattare il [team di supporto client di SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html).</span><span class="sxs-lookup"><span data-stu-id="7fb01-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="7fb01-164">Nella sezione **Attributi utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7fb01-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="7fb01-166">a.</span><span class="sxs-lookup"><span data-stu-id="7fb01-166">a.</span></span> <span data-ttu-id="7fb01-167">Nell'elenco **Identificatore utente** selezionare la funzione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="7fb01-168">b.</span><span class="sxs-lookup"><span data-stu-id="7fb01-168">b.</span></span> <span data-ttu-id="7fb01-169">Nell'elenco **Posta** selezionare l'attributo utente da usare per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="7fb01-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="7fb01-170">Ad esempio, se si vuole usare il valore EmployeeID come identificatore utente univoco e il valore dell'attributo è stato archiviato in ExtensionAttribute2, selezionare user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="7fb01-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="7fb01-171">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="7fb01-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7fb01-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7fb01-175">Nella sezione **Configurazione di SAP Cloud for Customer** fare clic su **Configura SAP Cloud for Customer** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7fb01-176">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="7fb01-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="7fb01-178">Per ottenere l'accesso SSO configurato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7fb01-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="7fb01-179">a.</span><span class="sxs-lookup"><span data-stu-id="7fb01-179">a.</span></span> <span data-ttu-id="7fb01-180">Accedere al portale di SAP Cloud for Customer con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7fb01-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="7fb01-181">b.</span><span class="sxs-lookup"><span data-stu-id="7fb01-181">b.</span></span> <span data-ttu-id="7fb01-182">Passare a **Attività comuni di gestione utenti e applicazioni** e fare clic sulla scheda **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="7fb01-183">c.</span><span class="sxs-lookup"><span data-stu-id="7fb01-183">c.</span></span> <span data-ttu-id="7fb01-184">Fare clic su **New Identity Provider** (Nuovo provider di identità) e selezionare il file XML dei metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb01-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="7fb01-185">Quando si importano i metadati, il sistema carica automaticamente il certificato di firma e il certificato di crittografia necessari.</span><span class="sxs-lookup"><span data-stu-id="7fb01-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="7fb01-187">d.</span><span class="sxs-lookup"><span data-stu-id="7fb01-187">d.</span></span> <span data-ttu-id="7fb01-188">Azure Active Directory richiede l'elemento URL del servizio consumer di asserzione nella richiesta SAML, quindi selezionare la casella di controllo **Include Assertion Consumer Service URL** (Includi URL del servizio Consumer di asserzione).</span><span class="sxs-lookup"><span data-stu-id="7fb01-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="7fb01-189">e.</span><span class="sxs-lookup"><span data-stu-id="7fb01-189">e.</span></span> <span data-ttu-id="7fb01-190">Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="7fb01-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="7fb01-191">f.</span><span class="sxs-lookup"><span data-stu-id="7fb01-191">f.</span></span> <span data-ttu-id="7fb01-192">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7fb01-192">Save your changes.</span></span>
   
    <span data-ttu-id="7fb01-193">g.</span><span class="sxs-lookup"><span data-stu-id="7fb01-193">g.</span></span> <span data-ttu-id="7fb01-194">Fare clic sulla scheda **My System** (Sistema locale).</span><span class="sxs-lookup"><span data-stu-id="7fb01-194">Click the **My System** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="7fb01-196">h.</span><span class="sxs-lookup"><span data-stu-id="7fb01-196">h.</span></span> <span data-ttu-id="7fb01-197">Nella casella di testo **URL di accesso di Azure AD** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb01-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="7fb01-199">i.</span><span class="sxs-lookup"><span data-stu-id="7fb01-199">i.</span></span> <span data-ttu-id="7fb01-200">Specificare se il dipendente può scegliere manualmente tra l'accesso con ID utente e password o SSO selezionando **Manual Identity Provider Selection**(Selezione manuale provider di identità).</span><span class="sxs-lookup"><span data-stu-id="7fb01-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="7fb01-201">j.</span><span class="sxs-lookup"><span data-stu-id="7fb01-201">j.</span></span> <span data-ttu-id="7fb01-202">Nella sezione **SSO URL** (URL SSO), specificare l'URL che deve essere usato dai dipendenti per l'accesso al sistema.</span><span class="sxs-lookup"><span data-stu-id="7fb01-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="7fb01-203">Nell'elenco **URL Sent to Employee** (URL inviato al dipendente) è possibile scegliere tra le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7fb01-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="7fb01-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="7fb01-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="7fb01-205">Il sistema invia al dipendente solo il normale URL di sistema.</span><span class="sxs-lookup"><span data-stu-id="7fb01-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="7fb01-206">Il dipendente non può accedere con SSO e deve usare invece la password o il certificato.</span><span class="sxs-lookup"><span data-stu-id="7fb01-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="7fb01-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="7fb01-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="7fb01-208">Il sistema invia al dipendente solo l'URL SSO.</span><span class="sxs-lookup"><span data-stu-id="7fb01-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="7fb01-209">Il dipendente può accedere con SSO.</span><span class="sxs-lookup"><span data-stu-id="7fb01-209">The employee can log on using SSO.</span></span> <span data-ttu-id="7fb01-210">La richiesta di autenticazione viene reindirizzata tramite IdP.</span><span class="sxs-lookup"><span data-stu-id="7fb01-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="7fb01-211">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="7fb01-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="7fb01-212">Se SSO non è attivo, il sistema invia al dipendente il normale URL di sistema.</span><span class="sxs-lookup"><span data-stu-id="7fb01-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="7fb01-213">Se SSO è attivo, il sistema verifica se il dipendente ha una password.</span><span class="sxs-lookup"><span data-stu-id="7fb01-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="7fb01-214">Se è disponibile una password, vengono inviati al dipendente sia l'URL SSO che l'URL non SSO.</span><span class="sxs-lookup"><span data-stu-id="7fb01-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="7fb01-215">Tuttavia, se il dipendente non ha una password, riceverà solo l'URL SSO.</span><span class="sxs-lookup"><span data-stu-id="7fb01-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="7fb01-216">k.</span><span class="sxs-lookup"><span data-stu-id="7fb01-216">k.</span></span> <span data-ttu-id="7fb01-217">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7fb01-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="7fb01-218">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7fb01-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7fb01-219">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7fb01-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7fb01-220">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fb01-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fb01-221">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fb01-222">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb01-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7fb01-224">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7fb01-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb01-225">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7fb01-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fb01-227">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7fb01-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fb01-229">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fb01-231">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7fb01-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fb01-233">a.</span><span class="sxs-lookup"><span data-stu-id="7fb01-233">a.</span></span> <span data-ttu-id="7fb01-234">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fb01-235">b.</span><span class="sxs-lookup"><span data-stu-id="7fb01-235">b.</span></span> <span data-ttu-id="7fb01-236">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7fb01-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fb01-237">c.</span><span class="sxs-lookup"><span data-stu-id="7fb01-237">c.</span></span> <span data-ttu-id="7fb01-238">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7fb01-239">d.</span><span class="sxs-lookup"><span data-stu-id="7fb01-239">d.</span></span> <span data-ttu-id="7fb01-240">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="7fb01-241">Creazione di un utente di test di SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="7fb01-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="7fb01-242">In questa sezione viene creato un utente di nome Britta Simon in SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="7fb01-243">Per aggiungere gli utenti nella piattaforma SAP Cloud for Customer, contattare il [team di supporto di SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html).</span><span class="sxs-lookup"><span data-stu-id="7fb01-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="7fb01-244">Assicurarsi che il valore di NameID corrisponda al campo username nella piattaforma SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7fb01-245">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb01-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7fb01-246">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7fb01-248">**Per assegnare Britta Simon a SAP Cloud for Customer, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7fb01-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb01-249">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7fb01-251">Nell'elenco delle applicazioni, selezionare **SAP Cloud for Customer**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="7fb01-253">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7fb01-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7fb01-255">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-255">Click **Add** button.</span></span> <span data-ttu-id="7fb01-256">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7fb01-258">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7fb01-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7fb01-259">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fb01-260">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7fb01-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fb01-261">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7fb01-261">Testing single sign-on</span></span>

<span data-ttu-id="7fb01-262">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7fb01-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7fb01-263">Quando si fa clic sul riquadro SAP Cloud for Customer nel pannello di accesso, si accederà automaticamente all'applicazione SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="7fb01-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="7fb01-264">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fb01-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fb01-265">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7fb01-265">Additional resources</span></span>

* [<span data-ttu-id="7fb01-266">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fb01-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fb01-267">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fb01-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

