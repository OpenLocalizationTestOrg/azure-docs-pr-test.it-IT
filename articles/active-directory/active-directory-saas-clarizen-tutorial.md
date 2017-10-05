---
title: 'Esercitazione: Integrazione di Azure Active Directory con Clarizen | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="07335-103">Esercitazione: Integrazione di Azure Active Directory con Clarizen</span><span class="sxs-lookup"><span data-stu-id="07335-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="07335-104">Questa esercitazione descrive come integrare Azure Active Directory (Azure AD) con Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="07335-105">Questa integrazione offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07335-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="07335-106">È possibile controllare in Azure AD chi può accedere a Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="07335-107">È possibile abilitare gli utenti per l'accesso automatico a Clarizen (Single Sign-On) con gli account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="07335-108">È possibile gestire gli account da una posizione centrale, il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="07335-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="07335-109">Lo scenario in questa esercitazione prevede due attività principali:</span><span class="sxs-lookup"><span data-stu-id="07335-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="07335-110">Aggiungere Clarizen dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="07335-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="07335-111">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="07335-112">Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07335-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07335-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="07335-113">Prerequisites</span></span>
<span data-ttu-id="07335-114">Per configurare l'integrazione di Azure AD con Clarizen, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="07335-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="07335-115">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-115">An Azure AD subscription</span></span>
- <span data-ttu-id="07335-116">Una sottoscrizione di Clarizen abilitata per Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07335-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="07335-117">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="07335-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="07335-118">Testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="07335-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07335-119">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="07335-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="07335-120">Se non è disponibile un ambiente di test di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07335-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="07335-121">Aggiungere Clarizen dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="07335-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="07335-122">Per configurare l'integrazione di Clarizen in Azure AD, aggiungere Clarizen dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="07335-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="07335-123">Nel [portale di Azure](https://portal.azure.com) fare clic sull'icona **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="07335-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icona Azure Active Directory][1]

2. <span data-ttu-id="07335-125">Fare clic su **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="07335-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="07335-126">Fare quindi clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07335-126">Then click **All applications**.</span></span>

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][2]

3. <span data-ttu-id="07335-128">Fare clic sul pulsante **Aggiungi** nella parte inferiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07335-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![Pulsante "Aggiungi"][3]

4. <span data-ttu-id="07335-130">Nella casella di ricerca digitare **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="07335-130">In the search box, type **Clarizen**.</span></span>

    ![Digitare "Clarizen" nella casella di ricerca](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="07335-132">Nel riquadro dei risultati selezionare **Clarizen** e quindi fare clic su **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07335-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Selezione di Clarizen nel riquadro dei risultati](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="07335-134">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07335-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="07335-135">Nelle sezioni seguenti viene configurato e testato l'accesso Single Sign-On di Azure AD con Clarizen con un utente di test di nome Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07335-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="07335-136">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Clarizen che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="07335-137">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="07335-138">La relazione di collegamento viene stabilita assegnando al valore **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="07335-139">Per configurare e testare l'accesso Single Sign-On di Azure AD con Clarizen, completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="07335-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="07335-140">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)** per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="07335-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07335-141">**[Creare un utente test di Azure AD](#create-an-azure-ad-test-user)** per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07335-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07335-142">**[Creare un utente di test di Clarizen](#create-a-clarizen-test-user)** per avere una controparte di Britta Simon in Clarizen collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="07335-143">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)** per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07335-144">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="07335-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="07335-145">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07335-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="07335-146">Abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure e configurare l'accesso Single Sign-On nell'applicazione Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="07335-147">Nella pagina di integrazione dell'applicazione **Clarizen** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="07335-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clic su "Single Sign-On"][4]

2. <span data-ttu-id="07335-149">Nella finestra di dialogo **Single Sign-On** per **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="07335-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Selezione di "Accesso basato su SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="07335-151">Nella sezione **URL e dominio Clarizen** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07335-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Caselle per identificatore e URL di risposta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="07335-153">a.</span><span class="sxs-lookup"><span data-stu-id="07335-153">a.</span></span> <span data-ttu-id="07335-154">Nella casella **Identificatore** digitare il valore **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="07335-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="07335-155">b.</span><span class="sxs-lookup"><span data-stu-id="07335-155">b.</span></span> <span data-ttu-id="07335-156">Nella casella **URL di risposta** digitare un URL usando il modello seguente: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="07335-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="07335-157">Questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="07335-157">These are not the real values.</span></span> <span data-ttu-id="07335-158">È necessario usare l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="07335-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="07335-159">In questo caso è consigliabile usare come identificatore il valore univoco di una stringa.</span><span class="sxs-lookup"><span data-stu-id="07335-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="07335-160">Per ottenere i valori effettivi, contattare il [team di supporto Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="07335-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="07335-161">Nella sezione **Certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="07335-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clic su "Crea nuovo certificato"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="07335-163">Nella finestra di dialogo **Crea nuovo certificato** fare clic sull'icona del calendario e selezionare una data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="07335-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="07335-164">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="07335-164">Then click **Save**.</span></span>

    ![Selezione e salvataggio di una data di scadenza](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="07335-166">Nella sezione **Certificato di firma SAML** selezionare **Rendi attivo il certificato nuovo** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="07335-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selezione della casella di controllo per rendere attivo il certificato nuovo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="07335-168">Nella finestra di dialogo **Certificato di rollover** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="07335-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clic su "OK" per confermare che si vuole rendere attivo il certificato](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="07335-170">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="07335-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Clic su "Certificato (Base64)" per avviare il download](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="07335-172">Nella sezione **Configurazione di Clarizen** fare clic su **Configura Clarizen** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="07335-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Clic su "Configure Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Finestra "Configura accesso", con i file e gli URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="07335-175">In un'altra finestra del Web browser accedere al sito aziendale di Clarizen come amministratore.</span><span class="sxs-lookup"><span data-stu-id="07335-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="07335-176">Fare clic sul nome utente e quindi su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="07335-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="07335-177">![Clic su "Settings" (Impostazioni) sotto il nome utente](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings (Impostazioni)")</span><span class="sxs-lookup"><span data-stu-id="07335-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="07335-178">Fare clic sulla scheda **Global Settings** (Impostazioni globali),</span><span class="sxs-lookup"><span data-stu-id="07335-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="07335-179">quindi accanto a **Federated Authentication** (Autenticazione federata) fare clic su **edit** (modifica).</span><span class="sxs-lookup"><span data-stu-id="07335-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="07335-180">![Scheda "Global Settings" (Impostazioni globali)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings (Impostazioni globali)")</span><span class="sxs-lookup"><span data-stu-id="07335-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="07335-181">Nella finestra di dialogo **Federated Authentication** (Autenticazione federata) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07335-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="07335-182">![Finestra di dialogo "Federated Authentication"(Autenticazione federata)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication (Autenticazione federata)")</span><span class="sxs-lookup"><span data-stu-id="07335-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="07335-183">a.</span><span class="sxs-lookup"><span data-stu-id="07335-183">a.</span></span> <span data-ttu-id="07335-184">Selezionare **Enable Federated Authentication** (Abilita autenticazione federata).</span><span class="sxs-lookup"><span data-stu-id="07335-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="07335-185">b.</span><span class="sxs-lookup"><span data-stu-id="07335-185">b.</span></span> <span data-ttu-id="07335-186">Per caricare il certificato scaricato, fare clic su **Carica** .</span><span class="sxs-lookup"><span data-stu-id="07335-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="07335-187">c.</span><span class="sxs-lookup"><span data-stu-id="07335-187">c.</span></span> <span data-ttu-id="07335-188">Nella casella di testo **Sign-in URL** (URL di accesso) immettere il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) dalla finestra di configurazione dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="07335-189">d.</span><span class="sxs-lookup"><span data-stu-id="07335-189">d.</span></span> <span data-ttu-id="07335-190">Nella casella **Sign-out URL** (URL di disconnessione) immettere il valore di **Sign-Out URL** (URL di disconnessione) dalla finestra di configurazione dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07335-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="07335-191">e.</span><span class="sxs-lookup"><span data-stu-id="07335-191">e.</span></span> <span data-ttu-id="07335-192">Selezionare **Utilizza POST**.</span><span class="sxs-lookup"><span data-stu-id="07335-192">Select **Use POST**.</span></span>

    <span data-ttu-id="07335-193">f.</span><span class="sxs-lookup"><span data-stu-id="07335-193">f.</span></span> <span data-ttu-id="07335-194">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="07335-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="07335-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07335-195">Create an Azure AD test user</span></span>
<span data-ttu-id="07335-196">Nel portale di Azure creare un utente di test chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07335-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Nome e indirizzo di posta elettronica dell'utente di test di Azure AD][100]

1. <span data-ttu-id="07335-198">Nel portale di Azure fare clic sull'icona **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="07335-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icona Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="07335-200">Fare clic su **Utenti e gruppi** e quindi su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="07335-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Clic su "Utenti e gruppi" e su "Tutti gli utenti"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="07335-202">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="07335-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![Pulsante "Aggiungi"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="07335-204">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07335-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo "Utente" con nome, indirizzo di posta elettronica e password inseriti](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="07335-206">a.</span><span class="sxs-lookup"><span data-stu-id="07335-206">a.</span></span> <span data-ttu-id="07335-207">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07335-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07335-208">b.</span><span class="sxs-lookup"><span data-stu-id="07335-208">b.</span></span> <span data-ttu-id="07335-209">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07335-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="07335-210">c.</span><span class="sxs-lookup"><span data-stu-id="07335-210">c.</span></span> <span data-ttu-id="07335-211">Selezionare **Mostra password** e prendere nota del valore di **Password**.</span><span class="sxs-lookup"><span data-stu-id="07335-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="07335-212">d.</span><span class="sxs-lookup"><span data-stu-id="07335-212">d.</span></span> <span data-ttu-id="07335-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="07335-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="07335-214">Creare un utente di test di Clarizen</span><span class="sxs-lookup"><span data-stu-id="07335-214">Create a Clarizen test user</span></span>
<span data-ttu-id="07335-215">Per consentire agli utenti di Azure AD di accedere a Clarizen, è necessario effettuare il provisioning degli account utente.</span><span class="sxs-lookup"><span data-stu-id="07335-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="07335-216">Nel caso di Clarizen, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="07335-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="07335-217">Accedere al sito aziendale di Clarizen come amministratore.</span><span class="sxs-lookup"><span data-stu-id="07335-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="07335-218">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="07335-218">Click **People**.</span></span>

    <span data-ttu-id="07335-219">![Clic su "People" (Persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People (Persone)")</span><span class="sxs-lookup"><span data-stu-id="07335-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="07335-220">Fare clic su **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="07335-220">Click **Invite User**.</span></span>

    <span data-ttu-id="07335-221">![Pulsante "Invite User" (Invita l'utente)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="07335-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="07335-222">Nella finestra di dialogo **Invite People** (Invita persone) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="07335-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="07335-223">![Finestra di dialogo "Invite People" (Invita persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People (Invita persone)")</span><span class="sxs-lookup"><span data-stu-id="07335-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="07335-224">a.</span><span class="sxs-lookup"><span data-stu-id="07335-224">a.</span></span> <span data-ttu-id="07335-225">Nella casella **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07335-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="07335-226">b.</span><span class="sxs-lookup"><span data-stu-id="07335-226">b.</span></span> <span data-ttu-id="07335-227">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="07335-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="07335-228">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="07335-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="07335-229">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07335-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="07335-230">Consentire a Britta Simon di usare l'accesso Single Sign-On di Azure concedendole l'accesso a Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Utente di test assegnato][200]

1. <span data-ttu-id="07335-232">Nel portale di Azure aprire la visualizzazione applicazioni, passare alla visualizzazione directory, fare clic su **Applicazioni aziendali** e quindi su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="07335-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][201]

2. <span data-ttu-id="07335-234">Nell'elenco delle applicazioni, selezionare **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="07335-234">In the applications list, select **Clarizen**.</span></span>

    ![Selezione di Clarizen nell'elenco](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="07335-236">Scegliere **Utenti e gruppi** nel riquadro a sinistra.</span><span class="sxs-lookup"><span data-stu-id="07335-236">In the left pane, click **Users and groups**.</span></span>

    ![Clic su "Utenti e gruppi"][202]

4. <span data-ttu-id="07335-238">Fare clic su **Add** .</span><span class="sxs-lookup"><span data-stu-id="07335-238">Click the **Add** button.</span></span> <span data-ttu-id="07335-239">Nella finestra di dialogo **Aggiungi assegnazione** selezionare quindi **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="07335-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Pulsante "Aggiungi" e finestra di dialogo "Aggiungi assegnazione"][203]

5. <span data-ttu-id="07335-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="07335-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="07335-242">Nella finestra di dialogo **Utenti e gruppi** fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="07335-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="07335-243">Nella finestra di dialogo **Aggiungi assegnazione** fare clic sul pulsante **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="07335-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="07335-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="07335-244">Test single sign-on</span></span>
<span data-ttu-id="07335-245">Testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="07335-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="07335-246">Quando si fa clic sul riquadro Clarizen nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Clarizen.</span><span class="sxs-lookup"><span data-stu-id="07335-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07335-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="07335-247">Additional resources</span></span>

* [<span data-ttu-id="07335-248">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07335-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07335-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07335-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
