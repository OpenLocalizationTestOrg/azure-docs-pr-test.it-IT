---
title: 'Esercitazione: Integrazione di Azure Active Directory con Envoy | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Envoy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="f517d-103">Esercitazione: Integrazione di Azure Active Directory con Envoy</span><span class="sxs-lookup"><span data-stu-id="f517d-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="f517d-104">Questa esercitazione descrive come integrare Envoy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f517d-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f517d-105">L'integrazione di Envoy con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f517d-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f517d-106">È possibile controllare in Azure AD chi può accedere a Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="f517d-107">È possibile abilitare gli utenti per l'accesso automatico a Envoy (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f517d-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f517d-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f517d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f517d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f517d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f517d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f517d-110">Prerequisites</span></span>

<span data-ttu-id="f517d-111">Per configurare l'integrazione di Azure AD con Envoy, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f517d-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="f517d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f517d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f517d-113">Sottoscrizione di Envoy abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f517d-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f517d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f517d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f517d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f517d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f517d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f517d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f517d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f517d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f517d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f517d-118">Scenario description</span></span>
<span data-ttu-id="f517d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f517d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f517d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f517d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f517d-121">Aggiunta di Envoy dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f517d-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="f517d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f517d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="f517d-123">Aggiunta di Envoy dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f517d-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="f517d-124">Per configurare l'integrazione di Envoy in Azure AD, è necessario aggiungere Envoy dalla raccolta al proprio elenco delle app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f517d-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f517d-125">**Per aggiungere Envoy dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f517d-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f517d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f517d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="f517d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f517d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f517d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f517d-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="f517d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="f517d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="f517d-133">Nella casella di ricerca digitare **Envoy** selezionare **Envoy** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f517d-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy nell'elenco risultati](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f517d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f517d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f517d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Envoy in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f517d-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f517d-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Envoy che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f517d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="f517d-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="f517d-139">Per stabilire la relazione di collegamento, in Envoy assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="f517d-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f517d-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Envoy, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f517d-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f517d-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f517d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f517d-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f517d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f517d-143">**[Creare un utente test di Envoy](#create-an-envoy-test-user)**: per avere una controparte di Britta Simon in Envoy collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f517d-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f517d-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f517d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f517d-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f517d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f517d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f517d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f517d-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On con l'applicazione Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="f517d-148">**Per configurare Single Sign-On di Azure AD con Envoy, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f517d-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="f517d-149">Nella pagina di integrazione dell'applicazione **Envoy** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f517d-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="f517d-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f517d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="f517d-153">Nella sezione **URL e dominio Envoy** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f517d-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="f517d-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.Envoy.com`.</span><span class="sxs-lookup"><span data-stu-id="f517d-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f517d-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f517d-156">This value is not real.</span></span> <span data-ttu-id="f517d-157">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="f517d-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f517d-158">Per ottenere il valore contattare il [team di supporto clienti di Envoy](https://envoy.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f517d-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="f517d-159">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="f517d-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="f517d-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f517d-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f517d-163">Nella sezione **Configurazione di Envoy** fare clic su **Configura Envoy** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="f517d-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f517d-164">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f517d-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="f517d-166">In un'altra finestra del Web browser accedere al sito aziendale di Envoy come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f517d-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="f517d-167">Nel barra degli strumenti in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="f517d-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="f517d-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="f517d-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="f517d-169">Fare clic su **Azienda**.</span><span class="sxs-lookup"><span data-stu-id="f517d-169">Click **Company**.</span></span>

    <span data-ttu-id="f517d-170">![Azienda](./media/active-directory-saas-envoy-tutorial/ic776783.png "Azienda")</span><span class="sxs-lookup"><span data-stu-id="f517d-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="f517d-171">Fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f517d-171">Click **SAML**.</span></span>

    <span data-ttu-id="f517d-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="f517d-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="f517d-173">Nella sezione di configurazione **SAML Authentication** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f517d-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="f517d-174">![Autenticazione SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="f517d-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="f517d-175">Il valore dell'ID della sede centrale viene generato automaticamente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f517d-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="f517d-176">a.</span><span class="sxs-lookup"><span data-stu-id="f517d-176">a.</span></span> <span data-ttu-id="f517d-177">Nella casella di testo **Fingerprint** (Impronta digitale) incollare il valore **Identificazione personale** del certificato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f517d-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="f517d-178">b.</span><span class="sxs-lookup"><span data-stu-id="f517d-178">b.</span></span> <span data-ttu-id="f517d-179">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **IDENTITY PROVIDER HTTP SAML URL** (URL SAML HTTP DEL PROVIDER DI IDENTITÀ).</span><span class="sxs-lookup"><span data-stu-id="f517d-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="f517d-180">c.</span><span class="sxs-lookup"><span data-stu-id="f517d-180">c.</span></span> <span data-ttu-id="f517d-181">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="f517d-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f517d-182">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="f517d-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f517d-183">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f517d-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f517d-184">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f517d-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f517d-185">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f517d-185">Create an Azure AD test user</span></span>

<span data-ttu-id="f517d-186">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f517d-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="f517d-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f517d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f517d-189">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="f517d-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f517d-191">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f517d-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f517d-193">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f517d-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f517d-195">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f517d-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f517d-197">a.</span><span class="sxs-lookup"><span data-stu-id="f517d-197">a.</span></span> <span data-ttu-id="f517d-198">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f517d-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f517d-199">b.</span><span class="sxs-lookup"><span data-stu-id="f517d-199">b.</span></span> <span data-ttu-id="f517d-200">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f517d-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f517d-201">c.</span><span class="sxs-lookup"><span data-stu-id="f517d-201">c.</span></span> <span data-ttu-id="f517d-202">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="f517d-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f517d-203">d.</span><span class="sxs-lookup"><span data-stu-id="f517d-203">d.</span></span> <span data-ttu-id="f517d-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f517d-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="f517d-205">Creare un utente test di Envoy</span><span class="sxs-lookup"><span data-stu-id="f517d-205">Create an Envoy test user</span></span>

<span data-ttu-id="f517d-206">Non è necessaria alcuna attività di configurazione per il provisioning degli utenti in Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="f517d-207">Quando un utente assegnato prova ad accedere a Envoy usando il pannello di accesso, Envoy verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="f517d-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="f517d-208">Se l'account utente non è presente, Envoy lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f517d-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f517d-209">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f517d-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="f517d-210">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="f517d-212">**Per assegnare Britta Simon a Envoy, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f517d-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="f517d-213">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f517d-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f517d-215">Nell'elenco delle applicazioni selezionare **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="f517d-215">In the applications list, select **Envoy**.</span></span>

    ![Collegamento di Envoy nell'elenco delle applicazioni](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="f517d-217">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f517d-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="f517d-219">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f517d-219">Click **Add** button.</span></span> <span data-ttu-id="f517d-220">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f517d-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="f517d-222">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f517d-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f517d-223">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f517d-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f517d-224">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f517d-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f517d-225">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f517d-225">Test single sign-on</span></span>

<span data-ttu-id="f517d-226">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f517d-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f517d-227">Quando si fa clic sul riquadro Envoy nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Envoy.</span><span class="sxs-lookup"><span data-stu-id="f517d-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="f517d-228">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f517d-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f517d-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f517d-229">Additional resources</span></span>

* [<span data-ttu-id="f517d-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f517d-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f517d-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f517d-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

