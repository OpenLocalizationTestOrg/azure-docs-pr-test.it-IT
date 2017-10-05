---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix ShareFile | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="42a10-103">Esercitazione: Integrazione di Azure Active Directory con Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="42a10-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="42a10-104">Questa esercitazione descrive come integrare Citrix ShareFile con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42a10-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42a10-105">L'integrazione di Citrix ShareFile con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="42a10-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42a10-106">È possibile controllare in Azure AD chi può accedere a Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="42a10-107">È possibile abilitare gli utenti per l'accesso automatico a Citrix ShareFile (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="42a10-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="42a10-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42a10-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42a10-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="42a10-110">Prerequisites</span></span>

<span data-ttu-id="42a10-111">Per configurare l'integrazione di Azure AD con Citrix ShareFile, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="42a10-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="42a10-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42a10-113">Sottoscrizione di Citrix ShareFile abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="42a10-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42a10-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="42a10-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42a10-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="42a10-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42a10-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="42a10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42a10-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42a10-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42a10-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="42a10-118">Scenario description</span></span>
<span data-ttu-id="42a10-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="42a10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42a10-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="42a10-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42a10-121">Aggiungere Citrix ShareFile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="42a10-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="42a10-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a10-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="42a10-123">Aggiungere Citrix ShareFile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="42a10-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="42a10-124">Per configurare l'integrazione di Citrix ShareFile in Azure AD, è necessario aggiungere Citrix ShareFile dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="42a10-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42a10-125">**Per aggiungere Citrix ShareFile dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="42a10-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42a10-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="42a10-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="42a10-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="42a10-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42a10-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="42a10-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="42a10-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="42a10-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="42a10-133">Nella casella di ricerca digitare **Citrix ShareFile**, selezionare **Citrix ShareFile** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="42a10-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile nell'elenco risultati](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="42a10-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a10-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="42a10-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Citrix ShareFile in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42a10-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42a10-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Citrix ShareFile che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="42a10-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="42a10-139">Per stabilire la relazione di collegamento, in Citrix ShareFile assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="42a10-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42a10-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Citrix ShareFile, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="42a10-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42a10-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="42a10-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42a10-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42a10-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42a10-143">**[Creare un utente test di Citrix ShareFile](#create-a-citrix-sharefile-test-user)**: per avere una controparte di Britta Simon in Citrix ShareFile collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42a10-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42a10-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="42a10-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="42a10-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a10-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="42a10-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="42a10-148">**Per configurare Single Sign-On di Azure AD con Citrix ShareFile, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="42a10-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="42a10-149">Nella pagina di integrazione dell'applicazione **Citrix ShareFile** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="42a10-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="42a10-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="42a10-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="42a10-153">Nella sezione **Citrix ShareFile Domain and URLs** (URL e dominio Citrix ShareFile) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="42a10-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="42a10-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.sharefile.com/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="42a10-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42a10-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="42a10-156">This value is not real.</span></span> <span data-ttu-id="42a10-157">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="42a10-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="42a10-158">Per ottenere questo valore, contattare il [team di supporto clienti di Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html).</span><span class="sxs-lookup"><span data-stu-id="42a10-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="42a10-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="42a10-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="42a10-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="42a10-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42a10-163">Nel **Citrix ShareFile Configuration** (Configurazione di Citrix ShareFile) fare clic su **Configure Citrix ShareFile** (Configura Citrix ShareFile) per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="42a10-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42a10-164">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="42a10-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="42a10-166">In un'altra finestra del Web browser accedere al sito aziendale di **Citrix ShareFile** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="42a10-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="42a10-167">Nel barra degli strumenti in alto fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="42a10-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="42a10-168">Nel riquadro di spostamento sinistro selezionare **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="42a10-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="42a10-169">![Account amministratore](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account amministratore")</span><span class="sxs-lookup"><span data-stu-id="42a10-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="42a10-170">In **Basic Settings** della finestra di dialogo **Single Sign-On/ SAML 2.0 Configuration** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="42a10-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="42a10-171">![Single Sign-On](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="42a10-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="42a10-172">a.</span><span class="sxs-lookup"><span data-stu-id="42a10-172">a.</span></span> <span data-ttu-id="42a10-173">Fare clic su **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="42a10-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="42a10-174">b.</span><span class="sxs-lookup"><span data-stu-id="42a10-174">b.</span></span> <span data-ttu-id="42a10-175">Nella casella di testo **Your IDP Issuer/ Entity ID** (Autorità di certificazione IdP/ID entità) incollare il valore **SAML Entity ID** (ID entità SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="42a10-176">c.</span><span class="sxs-lookup"><span data-stu-id="42a10-176">c.</span></span> <span data-ttu-id="42a10-177">Fare clic su **Change** (Cambia) accanto al campo **X.509 Certificate** (Certificato X.509) e quindi caricare il certificato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="42a10-178">d.</span><span class="sxs-lookup"><span data-stu-id="42a10-178">d.</span></span> <span data-ttu-id="42a10-179">Nella casella di testo **URL di accesso** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="42a10-180">e.</span><span class="sxs-lookup"><span data-stu-id="42a10-180">e.</span></span> <span data-ttu-id="42a10-181">Nella casella di testo **Logout URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="42a10-182">Fare clic su **Save** nel portale di gestione di Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="42a10-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="42a10-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42a10-184">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="42a10-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42a10-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42a10-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="42a10-186">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a10-186">Create an Azure AD test user</span></span>

<span data-ttu-id="42a10-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="42a10-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="42a10-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="42a10-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42a10-190">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="42a10-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="42a10-192">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="42a10-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="42a10-194">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="42a10-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="42a10-196">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="42a10-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="42a10-198">a.</span><span class="sxs-lookup"><span data-stu-id="42a10-198">a.</span></span> <span data-ttu-id="42a10-199">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42a10-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42a10-200">b.</span><span class="sxs-lookup"><span data-stu-id="42a10-200">b.</span></span> <span data-ttu-id="42a10-201">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42a10-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="42a10-202">c.</span><span class="sxs-lookup"><span data-stu-id="42a10-202">c.</span></span> <span data-ttu-id="42a10-203">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="42a10-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="42a10-204">d.</span><span class="sxs-lookup"><span data-stu-id="42a10-204">d.</span></span> <span data-ttu-id="42a10-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="42a10-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="42a10-206">Creare un utente test di Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="42a10-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="42a10-207">Per consentire agli utenti di Azure AD di accedere a Citrix ShareFile, è necessario eseguirne il provisioning in Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="42a10-208">Nel caso di Citrix ShareFile, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="42a10-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="42a10-209">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="42a10-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="42a10-210">Accedere al tenant di **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="42a10-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="42a10-211">Fare clic su **Manage Users \> Manage Users Home \> + Create Employee** (Gestisci utenti > Gestisci home utenti > + Crea dipendente).</span><span class="sxs-lookup"><span data-stu-id="42a10-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="42a10-212">![Crea dipendente](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Crea dipendente")</span><span class="sxs-lookup"><span data-stu-id="42a10-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="42a10-213">Nella sezione **Informazioni di base** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="42a10-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="42a10-214">![Informazioni di base](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informazioni di base")</span><span class="sxs-lookup"><span data-stu-id="42a10-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="42a10-215">a.</span><span class="sxs-lookup"><span data-stu-id="42a10-215">a.</span></span> <span data-ttu-id="42a10-216">Nella casella di testo **Email Address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica di Britta Simon come **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="42a10-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="42a10-217">b.</span><span class="sxs-lookup"><span data-stu-id="42a10-217">b.</span></span> <span data-ttu-id="42a10-218">Nella casella di testo **First Name** (Nome) digitare il **nome** dell'utente come **Britta**.</span><span class="sxs-lookup"><span data-stu-id="42a10-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="42a10-219">c.</span><span class="sxs-lookup"><span data-stu-id="42a10-219">c.</span></span> <span data-ttu-id="42a10-220">Nella casella di testo **Last Name** (Cognome) digitare il **cognome** dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="42a10-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="42a10-221">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="42a10-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="42a10-222">Il titolare dell'account Azure AD riceverà un messaggio di posta elettronica e selezionerà un collegamento per confermare il proprio account prima che venga attivato. È possibile usare qualsiasi altro strumento di creazione di account utente Citrix ShareFile o qualsiasi API fornita da Citrix ShareFile per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a10-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="42a10-223">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a10-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="42a10-224">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure, tramite la concessione dell'accesso a Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="42a10-226">**Per assegnare Britta Simon a Citrix ShareFile, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="42a10-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="42a10-227">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="42a10-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="42a10-229">Nell'elenco delle applicazioni, selezionare **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="42a10-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Collegamento di Citrix ShareFile nell'elenco delle applicazioni](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="42a10-231">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="42a10-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="42a10-233">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="42a10-233">Click **Add** button.</span></span> <span data-ttu-id="42a10-234">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="42a10-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="42a10-236">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="42a10-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42a10-237">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="42a10-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42a10-238">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="42a10-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="42a10-239">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="42a10-239">Test single sign-on</span></span>

<span data-ttu-id="42a10-240">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="42a10-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42a10-241">Quando si fa clic sul riquadro Citrix ShareFile nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="42a10-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="42a10-242">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42a10-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42a10-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="42a10-243">Additional resources</span></span>

* [<span data-ttu-id="42a10-244">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42a10-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42a10-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42a10-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

