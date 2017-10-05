---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SAP Business ByDesign.
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
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="9010b-103">Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="9010b-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="9010b-104">Questa esercitazione descrive come integrare SAP Business ByDesign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9010b-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9010b-105">L'integrazione di SAP Business ByDesign con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9010b-106">È possibile controllare in Azure AD chi può accedere a SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="9010b-107">È possibile abilitare gli utenti per l'accesso automatico a SAP Business ByDesign (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="9010b-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9010b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9010b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9010b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9010b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9010b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9010b-110">Prerequisites</span></span>

<span data-ttu-id="9010b-111">Per configurare l'integrazione di Azure AD con SAP Business ByDesign, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="9010b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9010b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9010b-113">Sottoscrizione di SAP Business ByDesign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9010b-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9010b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9010b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9010b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9010b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9010b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9010b-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9010b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9010b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9010b-118">Scenario description</span></span>
<span data-ttu-id="9010b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9010b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9010b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9010b-121">Aggiunta di SAP Business ByDesign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9010b-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="9010b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9010b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="9010b-123">Aggiunta di SAP Business ByDesign dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9010b-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="9010b-124">Per configurare l'integrazione di SAP Business ByDesign in Azure AD, è necessario aggiungere SAP Business ByDesign dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9010b-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9010b-125">**Per aggiungere SAP Business ByDesign dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9010b-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9010b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9010b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="9010b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9010b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9010b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9010b-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="9010b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="9010b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="9010b-133">Nella casella di ricerca digitare **SAP Business ByDesign**, selezionare **SAP Business ByDesign** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9010b-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign nell'elenco risultati](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9010b-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9010b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9010b-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business ByDesign con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9010b-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9010b-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SAP Business ByDesign che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9010b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="9010b-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="9010b-139">Per stabilire la relazione di collegamento, in SAP Business ByDesign assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="9010b-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9010b-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con SAP Business ByDesign, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9010b-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9010b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9010b-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9010b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9010b-143">**[Creare un utente di test di SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**: per avere una controparte di Britta Simon in SAP Business ByDesign collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9010b-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9010b-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9010b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9010b-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="9010b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9010b-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9010b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9010b-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="9010b-148">**Per configurare l'accesso Single Sign-On di Azure AD con SAP Business ByDesign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9010b-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="9010b-149">Nella pagina di integrazione dell'applicazione **SAP Business ByDesign** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9010b-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9010b-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9010b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="9010b-153">Nella sezione **URL e dominio SAP Business ByDesign** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9010b-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="9010b-155">a.</span><span class="sxs-lookup"><span data-stu-id="9010b-155">a.</span></span> <span data-ttu-id="9010b-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<servername>.sapbydesign.com`.</span><span class="sxs-lookup"><span data-stu-id="9010b-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="9010b-157">b.</span><span class="sxs-lookup"><span data-stu-id="9010b-157">b.</span></span> <span data-ttu-id="9010b-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="9010b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9010b-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="9010b-159">These values are not real.</span></span> <span data-ttu-id="9010b-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="9010b-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9010b-161">Per ottenere questi valori, contattare il [team di supporto clienti di SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="9010b-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="9010b-162">Nella sezione **Attributi utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9010b-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![Sezione degli attributi di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="9010b-164">a.</span><span class="sxs-lookup"><span data-stu-id="9010b-164">a.</span></span> <span data-ttu-id="9010b-165">Nell'elenco **Identificatore utente** selezionare la funzione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="9010b-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="9010b-166">b.</span><span class="sxs-lookup"><span data-stu-id="9010b-166">b.</span></span> <span data-ttu-id="9010b-167">Nell'elenco **Posta** selezionare l'attributo utente da usare per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="9010b-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="9010b-168">Ad esempio, se si vuole usare il valore EmployeeID come identificatore utente univoco e il valore dell'attributo è stato archiviato in ExtensionAttribute2, selezionare user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="9010b-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="9010b-169">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="9010b-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="9010b-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9010b-171">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9010b-173">Nella sezione **Configurazione di SAP Business ByDesign** fare clic su **Configura SAP Business ByDesign** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="9010b-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9010b-174">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="9010b-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="9010b-176">Per ottenere l'accesso SSO configurato per l'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9010b-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="9010b-177">a.</span><span class="sxs-lookup"><span data-stu-id="9010b-177">a.</span></span> <span data-ttu-id="9010b-178">Accedere al portale di SAP Business ByDesign con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="9010b-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="9010b-179">b.</span><span class="sxs-lookup"><span data-stu-id="9010b-179">b.</span></span> <span data-ttu-id="9010b-180">Passare a **Application and User Management Common Task** (Attività comuni di gestione utenti e applicazioni) e fare clic sulla scheda **Identity Provider** (Provider di identità).</span><span class="sxs-lookup"><span data-stu-id="9010b-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="9010b-181">c.</span><span class="sxs-lookup"><span data-stu-id="9010b-181">c.</span></span> <span data-ttu-id="9010b-182">Fare clic su **New Identity Provider** (Nuovo provider di identità) e selezionare il file XML metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9010b-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="9010b-183">Quando si importano i metadati, il sistema carica automaticamente il certificato di firma e il certificato di crittografia necessari.</span><span class="sxs-lookup"><span data-stu-id="9010b-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="9010b-185">d.</span><span class="sxs-lookup"><span data-stu-id="9010b-185">d.</span></span> <span data-ttu-id="9010b-186">Per includere l'**URL del servizio consumer di asserzione** nella richiesta SAML, selezionare **Include Assertion Consumer Service URL** (Includi URL del servizio Consumer di asserzione).</span><span class="sxs-lookup"><span data-stu-id="9010b-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="9010b-187">e.</span><span class="sxs-lookup"><span data-stu-id="9010b-187">e.</span></span> <span data-ttu-id="9010b-188">Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="9010b-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="9010b-189">f.</span><span class="sxs-lookup"><span data-stu-id="9010b-189">f.</span></span> <span data-ttu-id="9010b-190">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9010b-190">Save your changes.</span></span>
   
    <span data-ttu-id="9010b-191">g.</span><span class="sxs-lookup"><span data-stu-id="9010b-191">g.</span></span> <span data-ttu-id="9010b-192">Fare clic sulla scheda **My System** (Sistema locale).</span><span class="sxs-lookup"><span data-stu-id="9010b-192">Click the **My System** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="9010b-194">h.</span><span class="sxs-lookup"><span data-stu-id="9010b-194">h.</span></span> <span data-ttu-id="9010b-195">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **Single Sign On URL** (URL di accesso Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9010b-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="9010b-197">i.</span><span class="sxs-lookup"><span data-stu-id="9010b-197">i.</span></span> <span data-ttu-id="9010b-198">Specificare se il dipendente può scegliere manualmente tra l'accesso con ID utente e password o SSO selezionando **Manual Identity Provider Selection**(Selezione manuale provider di identità).</span><span class="sxs-lookup"><span data-stu-id="9010b-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="9010b-199">j.</span><span class="sxs-lookup"><span data-stu-id="9010b-199">j.</span></span> <span data-ttu-id="9010b-200">Nella sezione **SSO URL** (URL SSO), specificare l'URL che deve essere usato dai dipendenti per l'accesso al sistema.</span><span class="sxs-lookup"><span data-stu-id="9010b-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="9010b-201">Nell'elenco a discesa URL Sent to Employee (URL inviato al dipendente) è possibile scegliere tra le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9010b-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="9010b-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="9010b-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="9010b-203">Il sistema invia al dipendente solo il normale URL di sistema.</span><span class="sxs-lookup"><span data-stu-id="9010b-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="9010b-204">Il dipendente non può accedere con SSO e deve usare invece la password o il certificato.</span><span class="sxs-lookup"><span data-stu-id="9010b-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="9010b-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="9010b-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="9010b-206">Il sistema invia al dipendente solo l'URL SSO.</span><span class="sxs-lookup"><span data-stu-id="9010b-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="9010b-207">Il dipendente può accedere con SSO.</span><span class="sxs-lookup"><span data-stu-id="9010b-207">The employee can log on using SSO.</span></span> <span data-ttu-id="9010b-208">La richiesta di autenticazione viene reindirizzata tramite IdP.</span><span class="sxs-lookup"><span data-stu-id="9010b-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="9010b-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="9010b-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="9010b-210">Se SSO non è attivo, il sistema invia al dipendente il normale URL di sistema.</span><span class="sxs-lookup"><span data-stu-id="9010b-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="9010b-211">Se SSO è attivo, il sistema verifica se il dipendente ha una password.</span><span class="sxs-lookup"><span data-stu-id="9010b-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="9010b-212">Se è disponibile una password, vengono inviati al dipendente sia l'URL SSO che l'URL non SSO.</span><span class="sxs-lookup"><span data-stu-id="9010b-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="9010b-213">Tuttavia, se il dipendente non ha una password, riceverà solo l'URL SSO.</span><span class="sxs-lookup"><span data-stu-id="9010b-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="9010b-214">k.</span><span class="sxs-lookup"><span data-stu-id="9010b-214">k.</span></span> <span data-ttu-id="9010b-215">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9010b-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="9010b-216">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9010b-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9010b-217">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="9010b-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9010b-218">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9010b-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9010b-219">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9010b-219">Create an Azure AD test user</span></span>

<span data-ttu-id="9010b-220">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9010b-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="9010b-222">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9010b-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9010b-223">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="9010b-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9010b-225">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9010b-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9010b-227">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9010b-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9010b-229">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9010b-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9010b-231">a.</span><span class="sxs-lookup"><span data-stu-id="9010b-231">a.</span></span> <span data-ttu-id="9010b-232">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9010b-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9010b-233">b.</span><span class="sxs-lookup"><span data-stu-id="9010b-233">b.</span></span> <span data-ttu-id="9010b-234">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9010b-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9010b-235">c.</span><span class="sxs-lookup"><span data-stu-id="9010b-235">c.</span></span> <span data-ttu-id="9010b-236">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="9010b-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9010b-237">d.</span><span class="sxs-lookup"><span data-stu-id="9010b-237">d.</span></span> <span data-ttu-id="9010b-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9010b-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="9010b-239">Creare un utente di test di SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="9010b-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="9010b-240">In questa sezione viene creato un utente di nome Britta Simon in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="9010b-241">Collaborare con il [team di supporto clienti di SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) per aggiungere gli utenti nella piattaforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="9010b-242">Assicurarsi che il valore di NameID corrisponda al campo username nella piattaforma SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9010b-243">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9010b-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="9010b-244">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="9010b-246">**Per assegnare Britta Simon a SAP Business ByDesign, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9010b-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="9010b-247">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9010b-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9010b-249">Nell'elenco delle applicazioni, selezionare **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="9010b-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Collegamento di SAP Business ByDesign nell'elenco delle applicazioni](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="9010b-251">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9010b-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="9010b-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9010b-253">Click **Add** button.</span></span> <span data-ttu-id="9010b-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9010b-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="9010b-256">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="9010b-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9010b-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9010b-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9010b-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9010b-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9010b-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9010b-259">Test single sign-on</span></span>

<span data-ttu-id="9010b-260">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9010b-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9010b-261">Quando si fa clic sul riquadro SAP Business ByDesign nel pannello di accesso, si accederà automaticamente all'applicazione SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="9010b-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9010b-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9010b-262">Additional resources</span></span>

* [<span data-ttu-id="9010b-263">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9010b-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9010b-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9010b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

