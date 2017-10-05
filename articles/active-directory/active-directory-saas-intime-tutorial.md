---
title: 'Esercitazione: Integrazione di Azure Active Directory con InTime | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e InTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="81f43-103">Esercitazione: Integrazione di Azure Active Directory con InTime</span><span class="sxs-lookup"><span data-stu-id="81f43-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="81f43-104">Questa esercitazione descrive come integrare InTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81f43-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81f43-105">L'integrazione di InTime con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="81f43-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81f43-106">È possibile controllare in Azure AD chi può accedere a InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="81f43-107">È possibile abilitare gli utenti per l'accesso automatico a InTime (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="81f43-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="81f43-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="81f43-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="81f43-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81f43-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81f43-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="81f43-110">Prerequisites</span></span>

<span data-ttu-id="81f43-111">Per configurare l'integrazione di Azure AD con InTime, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="81f43-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="81f43-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81f43-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81f43-113">Sottoscrizione di InTime abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="81f43-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81f43-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="81f43-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81f43-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="81f43-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81f43-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="81f43-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81f43-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81f43-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81f43-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="81f43-118">Scenario description</span></span>
<span data-ttu-id="81f43-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="81f43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81f43-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="81f43-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81f43-121">Aggiunta di InTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="81f43-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="81f43-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f43-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="81f43-123">Aggiunta di InTime dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="81f43-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="81f43-124">Per configurare l'integrazione di InTime in Azure AD, è necessario aggiungere InTime dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="81f43-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81f43-125">**Per aggiungere InTime dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="81f43-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81f43-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="81f43-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="81f43-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="81f43-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81f43-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="81f43-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="81f43-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="81f43-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="81f43-133">Nella casella di ricerca digitare **InTime**, selezionare **InTime** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="81f43-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![InTime nell'elenco risultati](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="81f43-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f43-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="81f43-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con InTime usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81f43-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81f43-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di InTime corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81f43-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="81f43-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="81f43-139">Per stabilire la relazione di collegamento, in InTime assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="81f43-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81f43-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con InTime, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="81f43-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81f43-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="81f43-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81f43-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81f43-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81f43-143">**[Creare un utente di test di InTime](#create-a-intime-test-user)**: per avere una controparte di Britta Simon in InTime collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81f43-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81f43-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81f43-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81f43-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="81f43-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="81f43-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f43-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="81f43-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="81f43-148">**Per configurare l'accesso Single Sign-On di Azure AD con InTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="81f43-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="81f43-149">Nella pagina di integrazione dell'applicazione **InTime** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="81f43-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="81f43-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="81f43-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="81f43-153">Nella sezione **URL e dominio InTime** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="81f43-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="81f43-155">a.</span><span class="sxs-lookup"><span data-stu-id="81f43-155">a.</span></span> <span data-ttu-id="81f43-156">Nella casella di testo **URL accesso** digitare l'URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="81f43-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="81f43-157">b.</span><span class="sxs-lookup"><span data-stu-id="81f43-157">b.</span></span> <span data-ttu-id="81f43-158">Nella casella di testo **Identificatore** digitare l'URL: `https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="81f43-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="81f43-159">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="81f43-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="81f43-161">L'applicazione InTime si aspetta che le asserzioni SAML abbiano un formato specifico, quindi è necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="81f43-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="81f43-162">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="81f43-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="81f43-163">Il valore predefinito dell'**ID utente** è **user.userprincipalname** ma InTime si aspetta che venga mappato all'indirizzo e-mail dell'utente.</span><span class="sxs-lookup"><span data-stu-id="81f43-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="81f43-164">A tale scopo, è possibile usare l'attributo **user.mail** dall'elenco oppure usare il valore di attributo appropriato in base alla configurazione dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="81f43-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![Configurazione dell'attributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="81f43-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="81f43-166">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="81f43-168">Nella sezione **Configurazione di InTime** fare clic su **Configura InTime** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="81f43-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81f43-169">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="81f43-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="81f43-171">Per configurare l'accesso Single Sign-On sul lato **InTime**, è necessario inviare il file **XML metadati** scaricato, **l'URL di disconnessione e l'URL del servizio Single Sign-On SAML** al [team di supporto di InTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="81f43-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="81f43-172">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="81f43-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="81f43-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="81f43-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81f43-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="81f43-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81f43-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81f43-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="81f43-176">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f43-176">Create an Azure AD test user</span></span>

<span data-ttu-id="81f43-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="81f43-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="81f43-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="81f43-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81f43-180">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="81f43-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="81f43-182">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="81f43-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="81f43-184">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="81f43-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="81f43-186">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="81f43-186">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="81f43-188">a.</span><span class="sxs-lookup"><span data-stu-id="81f43-188">a.</span></span> <span data-ttu-id="81f43-189">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81f43-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81f43-190">b.</span><span class="sxs-lookup"><span data-stu-id="81f43-190">b.</span></span> <span data-ttu-id="81f43-191">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81f43-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="81f43-192">c.</span><span class="sxs-lookup"><span data-stu-id="81f43-192">c.</span></span> <span data-ttu-id="81f43-193">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="81f43-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="81f43-194">d.</span><span class="sxs-lookup"><span data-stu-id="81f43-194">d.</span></span> <span data-ttu-id="81f43-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="81f43-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="81f43-196">Creare un utente di test di InTime</span><span class="sxs-lookup"><span data-stu-id="81f43-196">Create a InTime test user</span></span>

<span data-ttu-id="81f43-197">In questa sezione viene creato un utente di nome Britta Simon in InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="81f43-198">Collaborare con il [team di supporto di InTime](mailto:hdollard@intimesoft.com) per aggiungere gli utenti alla piattaforma InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="81f43-199">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="81f43-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="81f43-200">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81f43-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="81f43-201">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="81f43-203">**Per assegnare Britta Simon a InTime, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="81f43-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="81f43-204">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="81f43-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="81f43-206">Nell'elenco delle applicazioni selezionare **InTime**.</span><span class="sxs-lookup"><span data-stu-id="81f43-206">In the applications list, select **InTime**.</span></span>

    ![Collegamento di InTime nell'elenco delle applicazioni](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="81f43-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="81f43-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="81f43-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="81f43-210">Click **Add** button.</span></span> <span data-ttu-id="81f43-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="81f43-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="81f43-213">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="81f43-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81f43-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="81f43-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81f43-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="81f43-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="81f43-216">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="81f43-216">Test single sign-on</span></span>

<span data-ttu-id="81f43-217">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="81f43-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81f43-218">Quando si fa clic sul riquadro InTime nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="81f43-219">Fare clic sul pulsante di **accesso** per visualizzare una serie di IdP in un elenco di pulsanti.</span><span class="sxs-lookup"><span data-stu-id="81f43-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="81f43-220">Fare clic sul **nome IDP** fornito dal [team di supporto di InTime](mailto:hdollard@intimesoft.com) per accedere all'applicazione InTime.</span><span class="sxs-lookup"><span data-stu-id="81f43-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="81f43-221">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81f43-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="81f43-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="81f43-222">Additional resources</span></span>

* [<span data-ttu-id="81f43-223">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81f43-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81f43-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81f43-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

