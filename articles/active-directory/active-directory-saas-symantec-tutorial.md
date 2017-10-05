---
title: 'Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Symantec Web Security Service (WSS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="6433c-103">Esercitazione: Integrazione di Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6433c-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="6433c-104">Questa esercitazione descrive come integrare l'account Symantec Web Security Service con l'account Azure Active Directory (Azure AD) in modo che WSS possa autenticare un utente finale di cui è stato effettuato il provisioning in Azure AD usando l'autenticazione SAML e applicare regole dei criteri a livello di utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="6433c-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="6433c-105">L'integrazione di Symantec Web Security Service (WSS) con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6433c-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6433c-106">Gestire tutti gli utenti finali e i gruppi usati dall'account WSS dal portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="6433c-107">Consentire agli utenti finali di autenticarsi in WSS usando le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="6433c-108">Abilitare l'applicazione delle regole dei criteri a livello di utente e gruppo definite nell'account WSS.</span><span class="sxs-lookup"><span data-stu-id="6433c-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="6433c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6433c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6433c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6433c-110">Prerequisites</span></span>

<span data-ttu-id="6433c-111">Per configurare l'integrazione di Azure AD con Symantec Web Security Service (WSS), sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6433c-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="6433c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6433c-113">Account Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6433c-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="6433c-114">Non è consigliabile usare un account WSS attualmente in uso nell'ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6433c-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="6433c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6433c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6433c-116">Non usare per i test un account WSS attualmente in uso nell'ambiente di produzione, a meno che ciò non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6433c-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="6433c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6433c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6433c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6433c-118">Scenario description</span></span>
<span data-ttu-id="6433c-119">In questa esercitazione si configurerà Azure AD per abilitare l'accesso Single Sign-On a WSS usando le credenziali dell'utente finale definite nell'account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="6433c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6433c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6433c-121">Aggiunta dell'app Symantec Web Security Service (WSS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6433c-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="6433c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6433c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="6433c-123">Aggiunta di Symantec Web Security Service (WSS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="6433c-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="6433c-124">Per configurare l'integrazione di Symantec Web Security Service (WSS) in Azure AD, è necessario aggiungere Symantec Web Security Service (WSS) dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6433c-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6433c-125">**Per aggiungere Symantec Web Security Service (WSS) dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6433c-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6433c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="6433c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="6433c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6433c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6433c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6433c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="6433c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="6433c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="6433c-133">Nella casella di ricerca digitare **Symantec Web Security Service (WSS)**, selezionare **Symantec Web Security Service (WSS)** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6433c-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![Symantec Web Security Service (WSS) nell'elenco risultati](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6433c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6433c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6433c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS) usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6433c-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6433c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Symantec Web Security Service (WSS) corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="6433c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6433c-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="6433c-139">Per stabilire la relazione di collegamento, in Symantec Web Security Service (WSS) assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="6433c-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6433c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS), è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="6433c-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6433c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6433c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6433c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6433c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6433c-143">**[Creare un utente di test di Symantec Web Security Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**: per avere una controparte di Britta Simon in Symantec Web Security Service (WSS) collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6433c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6433c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="6433c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6433c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6433c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6433c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6433c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="6433c-148">**Per configurare l'accesso Single Sign-On di Azure AD con Symantec Web Security Service (WSS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6433c-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="6433c-149">Nella pagina di integrazione dell'applicazione **Symantec Web Security Service (WSS)** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6433c-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6433c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6433c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="6433c-153">Nella sezione **URL e dominio Symantec Web Security Service (WSS)** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6433c-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="6433c-155">a.</span><span class="sxs-lookup"><span data-stu-id="6433c-155">a.</span></span> <span data-ttu-id="6433c-156">Nella casella di testo **Identificatore** digitare l'URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="6433c-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="6433c-157">b.</span><span class="sxs-lookup"><span data-stu-id="6433c-157">b.</span></span> <span data-ttu-id="6433c-158">Nella casella di testo **URL di risposta** digitare l'URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="6433c-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="6433c-159">Contattare il [team di supporto clienti di Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us) se per qualche motivo i valori **Identificatore** e **URL di risposta** non funzionano.</span><span class="sxs-lookup"><span data-stu-id="6433c-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="6433c-160">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="6433c-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="6433c-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6433c-162">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6433c-164">Per configurare l'accesso Single Sign-On sul lato Symantec Web Security Service (WSS), fare riferimento alla documentazione online di WSS.</span><span class="sxs-lookup"><span data-stu-id="6433c-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="6433c-165">Il file **XML metadati** scaricato dovrà essere importato nel portale di WSS.</span><span class="sxs-lookup"><span data-stu-id="6433c-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="6433c-166">Per assistenza per la configurazione nel portale di WSS, contattare il [team di supporto di Symantec Web Security Service (WSS)](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="6433c-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="6433c-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="6433c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6433c-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="6433c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6433c-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6433c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6433c-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6433c-170">Create an Azure AD test user</span></span>

<span data-ttu-id="6433c-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6433c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="6433c-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6433c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6433c-174">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="6433c-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6433c-176">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6433c-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6433c-178">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6433c-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6433c-180">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="6433c-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6433c-182">a.</span><span class="sxs-lookup"><span data-stu-id="6433c-182">a.</span></span> <span data-ttu-id="6433c-183">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6433c-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6433c-184">b.</span><span class="sxs-lookup"><span data-stu-id="6433c-184">b.</span></span> <span data-ttu-id="6433c-185">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6433c-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6433c-186">c.</span><span class="sxs-lookup"><span data-stu-id="6433c-186">c.</span></span> <span data-ttu-id="6433c-187">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="6433c-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6433c-188">d.</span><span class="sxs-lookup"><span data-stu-id="6433c-188">d.</span></span> <span data-ttu-id="6433c-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6433c-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="6433c-190">Creare un utente di test di Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="6433c-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="6433c-191">In questa sezione viene creato un utente di nome Britta Simon in Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6433c-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="6433c-192">Il nome utente corrispondente può essere creato manualmente nel portale di WSS oppure è possibile attendere alcuni minuti (circa 15) affinché venga eseguita la sincronizzazione con il portale di WSS degli utenti/gruppi di cui è stato effettuato il provisioning in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6433c-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="6433c-193">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="6433c-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="6433c-194">È anche necessario effettuare il provisioning nel portale di Symantec Web Security Service (WSS) dell'indirizzo IP pubblico del computer dell'utente finale che verrà usato per esplorare i siti Web.</span><span class="sxs-lookup"><span data-stu-id="6433c-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6433c-195">[Fare clic qui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) per ottenere l'indirizzo IP pubblico del computer.</span><span class="sxs-lookup"><span data-stu-id="6433c-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6433c-196">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6433c-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="6433c-197">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="6433c-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="6433c-199">**Per assegnare Britta Simon a Symantec Web Security Service (WSS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="6433c-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="6433c-200">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6433c-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6433c-202">Nell'elenco delle applicazioni selezionare **Symantec Web Security Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="6433c-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Collegamento di Symantec Web Security Service (WSS) nell'elenco delle applicazioni](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="6433c-204">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6433c-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="6433c-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6433c-206">Click **Add** button.</span></span> <span data-ttu-id="6433c-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6433c-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="6433c-209">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="6433c-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6433c-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6433c-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6433c-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6433c-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6433c-212">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6433c-212">Test single sign-on</span></span>

<span data-ttu-id="6433c-213">In questa sezione verrà testata la funzionalità Single Sign-On dopo aver configurato l'account WSS per l'uso di Azure AD per l'autenticazione SAML.</span><span class="sxs-lookup"><span data-stu-id="6433c-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="6433c-214">Dopo aver configurato il Web browser per inoltrare il traffico a WSS, quando si apre il Web browser e si prova a esplorare un sito, si viene reindirizzati alla pagina di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="6433c-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="6433c-215">Immettere le credenziali dell'utente finale di test di cui è stato effettuato il provisioning in Azure AD (ovvero BrittaSimon) e la password associata.</span><span class="sxs-lookup"><span data-stu-id="6433c-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="6433c-216">Una volta eseguita l'autenticazione, sarà possibile esplorare il sito Web scelto.</span><span class="sxs-lookup"><span data-stu-id="6433c-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="6433c-217">Se si crea una regola dei criteri sul lato WSS per impedire a BrittaSimon l'esplorazione di un sito specifico, quando si prova a esplorare tale sito come utente BrittaSimon viene visualizzata la pagina di blocco di WSS.</span><span class="sxs-lookup"><span data-stu-id="6433c-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6433c-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6433c-218">Additional resources</span></span>

* [<span data-ttu-id="6433c-219">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6433c-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6433c-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6433c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

