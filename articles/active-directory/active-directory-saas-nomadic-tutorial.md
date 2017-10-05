---
title: 'Esercitazione: Integrazione di Azure Active Directory con Nomadic | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Nomadic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 1817a1395c2ffa7268abfff268d9d041f7f21a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="3ca57-103">Esercitazione: integrazione di Azure Active Directory con Nomadic</span><span class="sxs-lookup"><span data-stu-id="3ca57-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="3ca57-104">Questa esercitazione descrive come integrare Nomadic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ca57-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ca57-105">L'integrazione di Nomadic con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ca57-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ca57-106">È possibile controllare in Azure AD chi può accedere a Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="3ca57-107">È possibile abilitare gli utenti per l'accesso automatico a Nomadic (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="3ca57-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3ca57-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca57-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3ca57-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ca57-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ca57-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3ca57-110">Prerequisites</span></span>

<span data-ttu-id="3ca57-111">Per configurare l'integrazione di Azure AD con Nomadic, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ca57-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="3ca57-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ca57-113">Sottoscrizione di Nomadic abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ca57-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ca57-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3ca57-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ca57-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ca57-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ca57-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3ca57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ca57-117">Se non si ha un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ca57-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ca57-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3ca57-118">Scenario description</span></span>
<span data-ttu-id="3ca57-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3ca57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ca57-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ca57-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ca57-121">Aggiungere Nomadic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ca57-121">Add Nomadic from the gallery</span></span>
2. <span data-ttu-id="3ca57-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca57-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="3ca57-123">Aggiungere Nomadic dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="3ca57-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="3ca57-124">Per configurare l'integrazione di Nomadic in Azure AD, è necessario aggiungere Nomadic dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3ca57-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ca57-125">**Per aggiungere Nomadic dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ca57-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca57-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ca57-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="3ca57-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ca57-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="3ca57-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ca57-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="3ca57-133">Nella casella di ricerca digitare **Nomadic**, selezionare **Nomadic** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ca57-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic nell'elenco risultati](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3ca57-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca57-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3ca57-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Nomadic in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ca57-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ca57-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Nomadic che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca57-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="3ca57-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="3ca57-139">Per stabilire la relazione di collegamento, in Nomadic assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="3ca57-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ca57-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Nomadic, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ca57-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ca57-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3ca57-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ca57-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca57-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ca57-143">**[Creare un utente di test di Nomadic](#create-a-nomadic-test-user)**: per avere una controparte di Britta Simon in Nomadic collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca57-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ca57-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca57-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ca57-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="3ca57-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3ca57-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca57-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3ca57-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="3ca57-148">**Per configurare Single Sign-On di Azure AD con Nomadic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ca57-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca57-149">Nella pagina di integrazione dell'applicazione **Nomadic** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="3ca57-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3ca57-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="3ca57-153">Nella sezione **URL e dominio Nomadic** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ca57-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="3ca57-155">a.</span><span class="sxs-lookup"><span data-stu-id="3ca57-155">a.</span></span> <span data-ttu-id="3ca57-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.nomadic.fm/signin`.</span><span class="sxs-lookup"><span data-stu-id="3ca57-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="3ca57-157">b.</span><span class="sxs-lookup"><span data-stu-id="3ca57-157">b.</span></span> <span data-ttu-id="3ca57-158">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="3ca57-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ca57-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="3ca57-159">These values are not real.</span></span> <span data-ttu-id="3ca57-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="3ca57-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3ca57-161">Per ottenere questi valori, contattare il [team di supporto clienti di Nomadic](mailto:help@nomadic.fm).</span><span class="sxs-lookup"><span data-stu-id="3ca57-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


4. <span data-ttu-id="3ca57-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="3ca57-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="3ca57-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3ca57-164">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="3ca57-166">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di Nomadic](mailto:help@nomadic.fm) e fornire i **metadati** scaricati.</span><span class="sxs-lookup"><span data-stu-id="3ca57-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="3ca57-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="3ca57-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ca57-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="3ca57-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ca57-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ca57-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3ca57-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca57-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3ca57-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca57-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="3ca57-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3ca57-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca57-174">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="3ca57-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3ca57-176">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3ca57-178">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3ca57-180">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ca57-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3ca57-182">a.</span><span class="sxs-lookup"><span data-stu-id="3ca57-182">a.</span></span> <span data-ttu-id="3ca57-183">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ca57-184">b.</span><span class="sxs-lookup"><span data-stu-id="3ca57-184">b.</span></span> <span data-ttu-id="3ca57-185">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca57-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3ca57-186">c.</span><span class="sxs-lookup"><span data-stu-id="3ca57-186">c.</span></span> <span data-ttu-id="3ca57-187">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3ca57-188">d.</span><span class="sxs-lookup"><span data-stu-id="3ca57-188">d.</span></span> <span data-ttu-id="3ca57-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="3ca57-190">Creare un utente test Nomadic</span><span class="sxs-lookup"><span data-stu-id="3ca57-190">Create a Nomadic test user</span></span>

<span data-ttu-id="3ca57-191">In questa sezione viene creato un utente di nome Britta Simon in Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="3ca57-192">Collaborare con il [team di supporto di Nomadic](mailto:help@nomadic.fm) per aggiungere gli utenti alla piattaforma Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3ca57-193">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca57-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="3ca57-194">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="3ca57-196">**Per assegnare Britta Simon a Nomadic, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="3ca57-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca57-197">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3ca57-199">Nell'elenco di applicazioni, selezionare **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-199">In the applications list, select **Nomadic**.</span></span>

    ![Collegamento di Nomadic nell'elenco delle applicazioni](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="3ca57-201">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3ca57-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="3ca57-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-203">Click **Add** button.</span></span> <span data-ttu-id="3ca57-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="3ca57-206">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="3ca57-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ca57-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ca57-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3ca57-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3ca57-209">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3ca57-209">Test single sign-on</span></span>

<span data-ttu-id="3ca57-210">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3ca57-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ca57-211">Quando si fa clic sul riquadro Nomadic nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Nomadic.</span><span class="sxs-lookup"><span data-stu-id="3ca57-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="3ca57-212">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ca57-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ca57-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3ca57-213">Additional resources</span></span>

* [<span data-ttu-id="3ca57-214">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca57-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ca57-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca57-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

