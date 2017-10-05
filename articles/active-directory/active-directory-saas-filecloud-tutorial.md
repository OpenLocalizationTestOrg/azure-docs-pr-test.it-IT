---
title: 'Esercitazione: Integrazione di Azure Active Directory con FileCloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FileCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="4ab8a-103">Esercitazione: Integrazione di Azure Active Directory con FileCloud</span><span class="sxs-lookup"><span data-stu-id="4ab8a-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="4ab8a-104">Questa esercitazione descrive come integrare FileCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ab8a-105">L'integrazione di FileCloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4ab8a-106">È possibile controllare in Azure AD chi può accedere a FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="4ab8a-107">È possibile abilitare gli utenti per l'accesso automatico a FileCloud (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4ab8a-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4ab8a-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ab8a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ab8a-110">Prerequisites</span></span>

<span data-ttu-id="4ab8a-111">Per configurare l'integrazione di Azure AD con FileCloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="4ab8a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ab8a-113">Sottoscrizione di FileCloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ab8a-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ab8a-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ab8a-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ab8a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ab8a-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ab8a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4ab8a-118">Scenario description</span></span>
<span data-ttu-id="4ab8a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ab8a-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ab8a-121">Aggiunta di FileCloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4ab8a-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="4ab8a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ab8a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="4ab8a-123">Aggiunta di FileCloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4ab8a-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="4ab8a-124">Per configurare l'integrazione di FileCloud in Azure AD, è necessario aggiungere FileCloud dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4ab8a-125">**Per aggiungere FileCloud dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4ab8a-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4ab8a-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="4ab8a-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4ab8a-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="4ab8a-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="4ab8a-133">Nella casella di ricerca digitare **FileCloud**, selezionare **FileCloud** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud nell'elenco dei risultati](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4ab8a-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ab8a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4ab8a-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FileCloud con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ab8a-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ab8a-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di FileCloud che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="4ab8a-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="4ab8a-139">Per stabilire la relazione di collegamento, in FileCloud assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4ab8a-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con FileCloud, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4ab8a-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4ab8a-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ab8a-143">**[Creare un utente di test di FileCloud](#create-a-filecloud-test-user)**: per avere una controparte di Britta Simon in FileCloud collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ab8a-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ab8a-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4ab8a-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ab8a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4ab8a-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="4ab8a-148">**Per configurare l'accesso Single Sign-On di Azure AD con FileCloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4ab8a-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4ab8a-149">Nella pagina di integrazione dell'applicazione **FileCloud** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurare il collegamento Single Sign-On][4]

2. <span data-ttu-id="4ab8a-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="4ab8a-153">Nella sezione **URL e dominio FileCloud** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="4ab8a-155">a.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-155">a.</span></span> <span data-ttu-id="4ab8a-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<subdomain>.filecloudhosted.com`.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="4ab8a-157">b.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-157">b.</span></span> <span data-ttu-id="4ab8a-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="4ab8a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ab8a-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4ab8a-159">These values are not real.</span></span> <span data-ttu-id="4ab8a-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4ab8a-161">Per ottenere questi valori, contattare il [team di supporto clienti di FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="4ab8a-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="4ab8a-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4ab8a-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4ab8a-166">Nella sezione **FileCloud Configuration** (Configurazione di FileCloud) fare clic su **Configure FileCloud** (Configura FileCloud) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4ab8a-167">Copiare l'**ID di entità SAML** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurazione di FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="4ab8a-169">In un'altra finestra del browser Web accedere al tenant FileCloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="4ab8a-170">Nella barra di spostamento a sinistra fare clic su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Sezione Settings (Impostazioni) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="4ab8a-172">Fare clic sulla scheda **SSO** nella sezione Settings (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Scheda SSO sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="4ab8a-174">Impostare **SAML** come **Default SSO Type** (Tipo SSO predefinito) nel riquadro **Single Sign On (SSO) Settings** (Impostazioni Single Sign-On - SSO).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Pannello Single Sign-On Settings (Impostazioni Single Sign-On - SSO) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="4ab8a-176">Incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure nella casella di testo **IdP End Point URL** (URL entità IdP).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Casella di testo IdP End Point URL (URL entità IdP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="4ab8a-178">Aprire il file di metadati scaricato in Blocco note, copiare i contenuti negli Appunti, quindi incollarli nella casella di testo **IdP Meta Data** (Metadati IdP) nel riquadro **SAML Settings** (Impostazioni SAML).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Sezione IdP Meta Data (Metadati IdP) sul lato dell'app](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="4ab8a-180">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4ab8a-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="4ab8a-181">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4ab8a-182">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4ab8a-183">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4ab8a-184">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ab8a-184">Create an Azure AD test user</span></span>

<span data-ttu-id="4ab8a-185">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="4ab8a-187">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ab8a-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4ab8a-188">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4ab8a-190">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4ab8a-192">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4ab8a-194">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4ab8a-194">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4ab8a-196">a.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-196">a.</span></span> <span data-ttu-id="4ab8a-197">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ab8a-198">b.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-198">b.</span></span> <span data-ttu-id="4ab8a-199">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4ab8a-200">c.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-200">c.</span></span> <span data-ttu-id="4ab8a-201">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4ab8a-202">d.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-202">d.</span></span> <span data-ttu-id="4ab8a-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="4ab8a-204">Creare un utente test di FileCloud</span><span class="sxs-lookup"><span data-stu-id="4ab8a-204">Create a FileCloud test user</span></span>

<span data-ttu-id="4ab8a-205">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="4ab8a-206">FileCloud supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4ab8a-207">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-207">There is no action item for you in this section.</span></span> <span data-ttu-id="4ab8a-208">Durante un tentativo di accesso a FileCloud viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4ab8a-209">Per creare un utente manualmente, è necessario contattare il [team di supporto clienti di FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="4ab8a-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4ab8a-210">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ab8a-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="4ab8a-211">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="4ab8a-213">**Per assegnare Britta Simon a FileCloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4ab8a-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4ab8a-214">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4ab8a-216">Nell'elenco delle applicazioni, selezionare **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-216">In the applications list, select **FileCloud**.</span></span>

    ![Collegamento FileCloud nell'elenco Applicazioni](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="4ab8a-218">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="4ab8a-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-220">Click **Add** button.</span></span> <span data-ttu-id="4ab8a-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="4ab8a-223">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4ab8a-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ab8a-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4ab8a-226">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ab8a-226">Test single sign-on</span></span>

<span data-ttu-id="4ab8a-227">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4ab8a-228">Quando si fa clic sul riquadro FileCloud nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4ab8a-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ab8a-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4ab8a-229">Additional resources</span></span>

* [<span data-ttu-id="4ab8a-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ab8a-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ab8a-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ab8a-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

