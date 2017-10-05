---
title: 'Esercitazione: Integrazione di Azure Active Directory con Help Scout | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Help Scout.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="2c591-103">Esercitazione: Integrazione di Azure Active Directory con Help Scout</span><span class="sxs-lookup"><span data-stu-id="2c591-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="2c591-104">Questa esercitazione descrive come integrare Help Scout con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2c591-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2c591-105">L'integrazione di Help Scout con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c591-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="2c591-106">In Azure AD è possibile controllare chi può accedere a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="2c591-107">È possibile connettere automaticamente gli utenti a Help Scout usando Single Sign-On e l'account Azure AD di un utente.</span><span class="sxs-lookup"><span data-stu-id="2c591-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="2c591-108">È possibile gestire gli account da una posizione centrale, il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c591-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="2c591-109">Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2c591-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c591-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2c591-110">Prerequisites</span></span>

<span data-ttu-id="2c591-111">Per configurare l'integrazione di Azure AD con Help Scout, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c591-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="2c591-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c591-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2c591-113">Sottoscrizione di Help Scout, con Single Sign-On attivato</span><span class="sxs-lookup"><span data-stu-id="2c591-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="2c591-114">Se si testano i passaggi di questa esercitazione, è consigliabile non testarli in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2c591-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="2c591-115">Raccomandazioni per il test dei passaggi di questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="2c591-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="2c591-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2c591-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="2c591-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c591-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2c591-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2c591-118">Scenario description</span></span>
<span data-ttu-id="2c591-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2c591-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="2c591-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c591-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2c591-121">Aggiungere Help Scout dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="2c591-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="2c591-122">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c591-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="2c591-123">Aggiungere Help Scout dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2c591-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="2c591-124">Per configurare l'integrazione di Help Scout con Azure AD, nella raccolta aggiungere Help Scout al proprio elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2c591-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2c591-125">Per aggiungere Help Scout dalla raccolta:</span><span class="sxs-lookup"><span data-stu-id="2c591-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="2c591-126">Nel [portale di Azure](https://portal.azure.com) fare clic su **Azure Active Directory** nel menu sinistro.</span><span class="sxs-lookup"><span data-stu-id="2c591-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="2c591-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2c591-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Pagina Applicazioni aziendali][2]
    
3. <span data-ttu-id="2c591-130">Per aggiungere una nuova applicazione, selezionare **Nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="2c591-130">To add a new application, select **New application**.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="2c591-132">Nella casella di ricerca immettere **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="2c591-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="2c591-133">Nei risultati della ricerca selezionare **Help Scout** e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2c591-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Help Scout nell'elenco risultati](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2c591-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c591-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="2c591-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Help Scout in base a un utente di test di nome *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="2c591-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="2c591-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di Azure AD in Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="2c591-138">Deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="2c591-139">Per stabilire la relazione di collegamento, in Help Scout per **Username** (Nome utente) assegnare il valore del **nome utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c591-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="2c591-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Help Scout, completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c591-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="2c591-141">[Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2c591-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="2c591-142">Configura un utente per l'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2c591-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="2c591-143">[Creare un utente test di Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="2c591-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="2c591-144">Testa l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c591-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="2c591-145">[Creare un utente di test di Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="2c591-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="2c591-146">Crea una controparte di Britta Simon in Help Scout collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c591-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="2c591-147">[Assegnare l'utente di test di Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="2c591-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="2c591-148">Configura Britta Simon per usare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c591-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2c591-149">[Testare l'accesso Single Sign-On](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2c591-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="2c591-150">Verifica se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2c591-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="2c591-151">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c591-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="2c591-152">In questa sezione si configura l'accesso Single Sign-On di Azure AD nel portale di Azure,</span><span class="sxs-lookup"><span data-stu-id="2c591-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="2c591-153">quindi si configura Single Sign-On nell'applicazione Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="2c591-154">Per configurare l'accesso Single Sign-On di Azure AD con Help Scout:</span><span class="sxs-lookup"><span data-stu-id="2c591-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="2c591-155">Nella pagina di integrazione dell'applicazione **Help Scout** del portale di Azure selezionare **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2c591-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Collegamento di configurazione di Single Sign-On][4]

2. <span data-ttu-id="2c591-157">Nella pagina **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML**.</span><span class="sxs-lookup"><span data-stu-id="2c591-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="2c591-159">In **URL e dominio Help Scout**, per configurare l'applicazione in modalità avviata da IDP, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2c591-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="2c591-160">Nella casella **Identificatore** immettere un URL con il modello seguente: `urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2c591-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="2c591-161">Nella casella **URL di risposta** immettere un URL con il modello seguente: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2c591-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="2c591-163">Se si preferisce configurare l'applicazione in modalità avviata da SP, selezionare la casella di controllo **Mostra impostazioni URL avanzate** e quindi seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2c591-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="2c591-164">Nella casella **URL di accesso** immettere un URL con il formato seguente: `https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="2c591-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="2c591-166">I valori in questi URL sono forniti solo a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="2c591-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="2c591-167">È necessario aggiornarli con l'URL dell'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="2c591-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="2c591-168">Per ottenere questi valori, contattare il [team di supporto di Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="2c591-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="2c591-169">In **Certificato di firma SAML** selezionare **XML metadati** e quindi salvare il file di metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="2c591-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="2c591-171">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2c591-171">Select **Save**.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2c591-173">Per configurare l'accesso Single Sign-On sul lato Help Scout, inviare il file XML di metadati scaricato al [team di supporto di Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="2c591-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="2c591-174">Il team di supporto di Help Scout applica questa impostazione in modo che la connessione Single Sign-On SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="2c591-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2c591-175">Un riepilogo delle istruzioni è disponibile nel [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="2c591-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="2c591-176">Dopo avere aggiunto l'app selezionando **Active Directory** > **Applicazioni aziendali**, selezionare la scheda **Single Sign-On**. È possibile accedere alla documentazione incorporata nella sezione **Configurazione** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="2c591-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="2c591-177">Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2c591-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2c591-178">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c591-178">Create an Azure AD test user</span></span>

<span data-ttu-id="2c591-179">In questa sezione viene creato un utente di test chiamato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c591-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="2c591-181">Per creare un utente di test in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="2c591-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="2c591-182">Nel portale di Azure fare clic su **Azure Active Directory** nel menu sinistro.</span><span class="sxs-lookup"><span data-stu-id="2c591-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2c591-184">Selezionare **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2c591-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Selezionare Utenti e gruppi e quindi selezionare Tutti gli utenti.](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2c591-186">Per aprire la finestra di dialogo **Utente**, nella parte superiore della pagina **Tutti gli utenti** selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2c591-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2c591-188">Nella finestra di dialogo **Utente** completare questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2c591-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="2c591-189">Nella casella **Nome** immettere **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2c591-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="2c591-190">Nella casella **Nome utente** immettere l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2c591-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="2c591-191">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="2c591-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="2c591-192">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2c591-192">Select **Create**.</span></span>

        ![Finestra di dialogo Utente](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="2c591-194">Creare un utente test di Help Scout</span><span class="sxs-lookup"><span data-stu-id="2c591-194">Create a Help Scout test user</span></span>

<span data-ttu-id="2c591-195">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="2c591-196">Help Scout supporta il provisioning JIT, che è attivato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2c591-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="2c591-197">In questa sezione non è necessario completare azioni o attività.</span><span class="sxs-lookup"><span data-stu-id="2c591-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="2c591-198">Se un utente non esiste in Help Scout, ne viene creato uno nuovo quando si prova ad accedere a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2c591-199">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c591-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="2c591-200">In questa sezione si consente all'utente Britta Simon di usare l'accesso Single Sign-On di Azure AD concedendo all'account utente l'accesso a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="2c591-202">Per assegnare Britta Simon a Help Scout:</span><span class="sxs-lookup"><span data-stu-id="2c591-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="2c591-203">Nel portale di Azure aprire la visualizzazione applicazioni e quindi passare alla visualizzazione directory.</span><span class="sxs-lookup"><span data-stu-id="2c591-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="2c591-204">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2c591-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2c591-206">Nell'elenco delle applicazioni selezionare **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="2c591-206">In the applications list, select **Help Scout**.</span></span>

    ![Collegamento di Help Scout nell'elenco delle applicazioni](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="2c591-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2c591-208">In the left menu, select **Users and groups**.</span></span>

    ![Collegamento Utenti e gruppi][202]

4. <span data-ttu-id="2c591-210">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2c591-210">Select **Add**.</span></span> <span data-ttu-id="2c591-211">Quindi nella pagina **Aggiungi assegnazione** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2c591-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="2c591-213">Nella pagina **Utenti e gruppi** selezionare **Britta Simon** nell'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="2c591-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="2c591-214">Nella pagina **Utenti e gruppi** selezionare **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2c591-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="2c591-215">Nella pagina **Aggiungi assegnazione** selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="2c591-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2c591-216">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2c591-216">Test single sign-on</span></span>

<span data-ttu-id="2c591-217">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2c591-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="2c591-218">Quando si seleziona il riquadro Help Scout nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Help Scout.</span><span class="sxs-lookup"><span data-stu-id="2c591-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="2c591-219">Per altre informazioni sul pannello di accesso, vedere [Introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2c591-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2c591-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2c591-220">Additional resources</span></span>

* [<span data-ttu-id="2c591-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c591-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c591-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c591-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

