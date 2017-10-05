---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cezanne HR Software | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Cezanne HR Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="c14c0-103">Esercitazione: Eseguire l'integrazione di Azure Active Directory con Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="c14c0-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="c14c0-104">Questa esercitazione descrive come integrare Cezanne HR Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c14c0-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c14c0-105">L'integrazione di Cezanne HR Software con Azure AD offre i vantaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c14c0-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="c14c0-106">È possibile:</span><span class="sxs-lookup"><span data-stu-id="c14c0-106">You can:</span></span>

- <span data-ttu-id="c14c0-107">È possibile controllare in Azure AD chi può accedere a Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="c14c0-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="c14c0-108">È possibile abilitare gli utenti per l'accesso automatico a Cezanne HR Software (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="c14c0-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c14c0-109">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c0-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="c14c0-110">Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c14c0-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c14c0-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c14c0-111">Prerequisites</span></span>

<span data-ttu-id="c14c0-112">Per configurare l'integrazione di Azure AD con Cezanne HR Software, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c14c0-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="c14c0-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14c0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c14c0-114">Sottoscrizione di Cezanne HR Software abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="c14c0-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c14c0-115">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c14c0-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="c14c0-116">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="c14c0-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c14c0-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c14c0-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c14c0-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c14c0-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c14c0-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c14c0-119">Scenario description</span></span>
<span data-ttu-id="c14c0-120">In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c14c0-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="c14c0-121">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c14c0-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="c14c0-122">Aggiunta di Cezanne HR Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c14c0-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="c14c0-123">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14c0-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="c14c0-124">Aggiungere Cezanne HR Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c14c0-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="c14c0-125">Per configurare l'integrazione di Cezanne HR Software in Azure AD, è necessario aggiungere Cezanne HR Software dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c14c0-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c14c0-126">Per aggiungere Cezanne HR Software dalla raccolta, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="c14c0-127">Nel **[portale di Azure](https://portal.azure.com)** fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="c14c0-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Pulsante "Azure Active Directory"][1]

2. <span data-ttu-id="c14c0-129">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Collegamento "Tutte le applicazioni"][2]
    
3. <span data-ttu-id="c14c0-131">Per aggiungere una nuova applicazione, fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    ![Pulsante "Nuova applicazione"][3]

4. <span data-ttu-id="c14c0-133">Nella casella di ricerca, digitare **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![Casella di ricerca](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="c14c0-135">Nell'elenco risultati selezionare **Cezanne HR Software** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c14c0-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![Elenco risultati](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c14c0-137">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14c0-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c14c0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cezanne HR Software usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c14c0-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c14c0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Cezanne HR Software corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c14c0-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="c14c0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="c14c0-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="c14c0-141">Per stabilire la relazione di collegamento, in Cezanne HR Software assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="c14c0-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="c14c0-142">Per configurare e testare l'accesso SSO di Azure AD con Cezanne HR Software, è necessario completare le procedure di base seguenti.</span><span class="sxs-lookup"><span data-stu-id="c14c0-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c14c0-143">Configurare l'accesso SSO di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14c0-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="c14c0-144">In questa sezione è possibile abilitare l'accesso SSO di Azure AD nel portale di Azure e configurare l'accesso SSO nell'applicazione Cezanne HR Software seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="c14c0-145">Nella pagina di integrazione dell'applicazione **Cezanne HR Software** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Comando "Single Sign-On"][4]

2. <span data-ttu-id="c14c0-147">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="c14c0-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Casella "Modalità"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="c14c0-149">In **URL e dominio Cezanne HR Software** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![Sezione "URL e dominio Cezanne HR Software"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="c14c0-151">a.</span><span class="sxs-lookup"><span data-stu-id="c14c0-151">a.</span></span> <span data-ttu-id="c14c0-152">Nella casella **URL di accesso** digitare un URL con la sintassi seguente: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="c14c0-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="c14c0-153">b.</span><span class="sxs-lookup"><span data-stu-id="c14c0-153">b.</span></span> <span data-ttu-id="c14c0-154">Nella casella **URL di risposta** digitare un URL con la sintassi seguente: `https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="c14c0-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="c14c0-155">I valori precedenti non sono valori reali.</span><span class="sxs-lookup"><span data-stu-id="c14c0-155">The preceding values are not real.</span></span> <span data-ttu-id="c14c0-156">Aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="c14c0-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="c14c0-157">Per ottenere questi valori, contattare il [team di supporto clienti di Cezanne HR Software](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="c14c0-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="c14c0-158">In **Certificato di firma SAML** selezionare **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c14c0-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Sezione "Certificato di firma SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="c14c0-160">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-160">Select **Save**.</span></span>

    ![Pulsante "Salva"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="c14c0-162">In **Configurazione di Cezanne HR Software** selezionare **Configura Cezanne HR Software** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="c14c0-163">Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![Sezione "Configurazione di Cezanne HR Software"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="c14c0-165">In un'altra finestra del Web browser accedere al tenant Cezanne HR Software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c14c0-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="c14c0-166">Nel riquadro sinistro selezionare **System Setup** (Configurazione di sistema).</span><span class="sxs-lookup"><span data-stu-id="c14c0-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="c14c0-167">Selezionare **Security Settings** > **Single Sign-On Configuration** (Impostazioni di sicurezza > Configurazione Single Sign-on).</span><span class="sxs-lookup"><span data-stu-id="c14c0-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Collegamento per la configurazione Single Sign-on](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="c14c0-169">Nel riquadro **Allow users to log in using the following Single Sign-On (SSO) Service** (Consenti agli utenti di accedere usando il servizio Single Sign-On (SSO) seguente) selezionare la casella di controllo **SAML 2.0** e quindi l'opzione **Advanced Configuration** (Configurazione avanzata).</span><span class="sxs-lookup"><span data-stu-id="c14c0-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Opzioni dei servizi Single Sign-On](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="c14c0-171">Selezionare **Add New** (Aggiungi nuovo).</span><span class="sxs-lookup"><span data-stu-id="c14c0-171">Select **Add New**.</span></span>

    ![Pulsante "Add New" (Aggiungi nuovo)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="c14c0-173">In **SAML 2.0 Identity Providers** (Provider di identità SAML 2.0) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![Sezione relativa ai provider di identità SAML 2.0](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="c14c0-175">a.</span><span class="sxs-lookup"><span data-stu-id="c14c0-175">a.</span></span> <span data-ttu-id="c14c0-176">Nella casella **Display Name**(Nome visualizzato) immettere il nome del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c14c0-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="c14c0-177">b.</span><span class="sxs-lookup"><span data-stu-id="c14c0-177">b.</span></span> <span data-ttu-id="c14c0-178">Nella casella **Entity Identifier** (Identificatore entità) incollare l'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c0-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="c14c0-179">c.</span><span class="sxs-lookup"><span data-stu-id="c14c0-179">c.</span></span> <span data-ttu-id="c14c0-180">Nella casella di riepilogo **SAML Binding** (Associazione SAML) selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="c14c0-181">d.</span><span class="sxs-lookup"><span data-stu-id="c14c0-181">d.</span></span> <span data-ttu-id="c14c0-182">Nella casella **Security Token Service Endpoint** (Endpoint del servizio token di sicurezza) incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c0-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="c14c0-183">e.</span><span class="sxs-lookup"><span data-stu-id="c14c0-183">e.</span></span> <span data-ttu-id="c14c0-184">Nella casella **User ID Attribute Name** (Nome attributo ID utente) immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="c14c0-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="c14c0-185">f.</span><span class="sxs-lookup"><span data-stu-id="c14c0-185">f.</span></span> <span data-ttu-id="c14c0-186">Per caricare il certificato scaricato da Azure AD, fare clic sul pulsante **Upload** (Carica).</span><span class="sxs-lookup"><span data-stu-id="c14c0-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="c14c0-187">g.</span><span class="sxs-lookup"><span data-stu-id="c14c0-187">g.</span></span> <span data-ttu-id="c14c0-188">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-188">Select **OK**.</span></span> 

12. <span data-ttu-id="c14c0-189">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-189">Select **Save**.</span></span>

    ![Pulsante "Salva"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="c14c0-191">Durante la configurazione dell'app, nel [portale di Azure](https://portal.azure.com) è disponibile un riepilogo delle istruzioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="c14c0-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c14c0-192">Dopo aver aggiunto l'app dalla sezione **Active Directory** > **Applicazioni aziendali**, selezionare la scheda **Single Sign-On**. Accedere quindi alla documentazione incorporata tramite la sezione **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="c14c0-193">Per altre informazioni sulla funzione di documentazione incorporata vedere [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c14c0-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c14c0-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14c0-194">Create an Azure AD test user</span></span>
<span data-ttu-id="c14c0-195">In questa sezione viene creato un utente di test di nome Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c14c0-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Utente di test Britta Simon][100]

<span data-ttu-id="c14c0-197">Per creare un utente di test in Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="c14c0-198">Nel **portale di Azure** fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="c14c0-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Pulsante "Azure Active Directory"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c14c0-200">Per visualizzare l'elenco di utenti, selezionare **Utenti e gruppi** > **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Collegamento "Tutti gli utenti"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="c14c0-202">Verrà visualizzata la finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="c14c0-203">Per aprire la finestra di dialogo **Utente**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Pulsante "Aggiungi"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c14c0-205">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-205">In the **User** dialog box, do the following:</span></span>
 
    ![Finestra di dialogo "Utente"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c14c0-207">a.</span><span class="sxs-lookup"><span data-stu-id="c14c0-207">a.</span></span> <span data-ttu-id="c14c0-208">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c14c0-209">b.</span><span class="sxs-lookup"><span data-stu-id="c14c0-209">b.</span></span> <span data-ttu-id="c14c0-210">Nella casella **Nome utente** digitare l'**indirizzo e-mail** dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c14c0-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="c14c0-211">c.</span><span class="sxs-lookup"><span data-stu-id="c14c0-211">c.</span></span> <span data-ttu-id="c14c0-212">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore generato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="c14c0-213">d.</span><span class="sxs-lookup"><span data-stu-id="c14c0-213">d.</span></span> <span data-ttu-id="c14c0-214">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="c14c0-215">Creare un utente di test di Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="c14c0-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="c14c0-216">Per consentire agli utenti di Azure AD di accedere a Cezanne HR Software, è necessario effettuarne il provisioning in Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="c14c0-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="c14c0-217">Nel caso di Cezanne HR Software, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c14c0-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="c14c0-218">Per effettuare il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="c14c0-219">Accedere al sito aziendale di Cezanne HR software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c14c0-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="c14c0-220">Nel riquadro sinistro selezionare **System Setup** > **Manage Users** > **Add New User** (Configurazione di sistema > Gestisci utenti > Aggiungi nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="c14c0-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="c14c0-221">![Collegamento per l'aggiunta di un nuovo utente](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="c14c0-222">In **Person Details** (Dettagli persona) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="c14c0-223">![Sezione relativa ai dettagli persona](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="c14c0-224">a.</span><span class="sxs-lookup"><span data-stu-id="c14c0-224">a.</span></span> <span data-ttu-id="c14c0-225">Impostare **Internal User** (Utente interno) su **OFF**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="c14c0-226">b.</span><span class="sxs-lookup"><span data-stu-id="c14c0-226">b.</span></span> <span data-ttu-id="c14c0-227">Nella casella **First Name** (Nome) digitare il nome dell'utente, ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="c14c0-228">c.</span><span class="sxs-lookup"><span data-stu-id="c14c0-228">c.</span></span> <span data-ttu-id="c14c0-229">Nella casella **Last Name** (Cognome) digitare il cognome dell'utente, ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="c14c0-230">d.</span><span class="sxs-lookup"><span data-stu-id="c14c0-230">d.</span></span> <span data-ttu-id="c14c0-231">Nella casella **E-mail** (Posta elettronica) digitare l'indirizzo e-mail dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c14c0-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="c14c0-232">In **Account Information** (Informazioni account) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c14c0-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="c14c0-233">![Sezione relativa alle informazioni account](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="c14c0-234">a.</span><span class="sxs-lookup"><span data-stu-id="c14c0-234">a.</span></span> <span data-ttu-id="c14c0-235">Nella casella **Username** (Nome utente) digitare l'indirizzo e-mail dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c14c0-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="c14c0-236">b.</span><span class="sxs-lookup"><span data-stu-id="c14c0-236">b.</span></span> <span data-ttu-id="c14c0-237">Nella casella **Password** digitare la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c14c0-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="c14c0-238">c.</span><span class="sxs-lookup"><span data-stu-id="c14c0-238">c.</span></span> <span data-ttu-id="c14c0-239">Nella casella **Security Role** (Ruolo di sicurezza) selezionare **HR Professional** (Professionista HR).</span><span class="sxs-lookup"><span data-stu-id="c14c0-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="c14c0-240">d.</span><span class="sxs-lookup"><span data-stu-id="c14c0-240">d.</span></span> <span data-ttu-id="c14c0-241">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-241">Select **OK**.</span></span>

5. <span data-ttu-id="c14c0-242">Nella scheda **Single Sign-On** selezionare **Add New** (Aggiungi nuovo) nella sezione **SAML 2.0 Identifiers** (Identificatori SAML 2.0).</span><span class="sxs-lookup"><span data-stu-id="c14c0-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="c14c0-243">![Pulsante "Add New" (Aggiungi nuovo)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="c14c0-244">Nella casella di riepilogo **Identity Provider** (Provider di identità) selezionare il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c14c0-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="c14c0-245">Nella casella **User Identifier** (Identificatore utente) immettere l'indirizzo e-mail dell'account dell'utente di test Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c14c0-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="c14c0-246">![Caselle relative a provider di identità e ID utente](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="c14c0-247">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-247">Select **Save**.</span></span>

    <span data-ttu-id="c14c0-248">![Pulsante di salvataggio](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Utente")</span><span class="sxs-lookup"><span data-stu-id="c14c0-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c14c0-249">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c14c0-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="c14c0-250">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="c14c0-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Accesso utente di test][200] 

1. <span data-ttu-id="c14c0-252">Nel portale di Azure aprire la visualizzazione applicazioni e quindi passare alla visualizzazione directory.</span><span class="sxs-lookup"><span data-stu-id="c14c0-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="c14c0-253">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Collegamento "Tutte le applicazioni"][201] 

2. <span data-ttu-id="c14c0-255">Nell'elenco di applicazioni selezionare **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Elenco "Applicazioni"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="c14c0-257">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c14c0-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Assegnare utenti][202] 

4. <span data-ttu-id="c14c0-259">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-259">Select **Add**.</span></span> <span data-ttu-id="c14c0-260">Nella finestra di dialogo **Aggiungi assegnazione** selezionare quindi **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][203]

5. <span data-ttu-id="c14c0-262">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="c14c0-263">Nella finestra di dialogo **Utenti e gruppi** fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="c14c0-264">Nella finestra di dialogo **Aggiungi assegnazione** selezionare **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="c14c0-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="c14c0-265">Testare l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="c14c0-265">Test SSO</span></span>

<span data-ttu-id="c14c0-266">In questa sezione viene testata la configurazione dell'accesso SSO di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c14c0-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="c14c0-267">Quando si fa clic sul riquadro Cezanne HR Software nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="c14c0-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c14c0-268">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c14c0-268">Next steps</span></span>

* [<span data-ttu-id="c14c0-269">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c14c0-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c14c0-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c14c0-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

