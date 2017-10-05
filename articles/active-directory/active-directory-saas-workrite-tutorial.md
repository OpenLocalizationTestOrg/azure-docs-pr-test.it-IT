---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workrite | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workrite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="72528-103">Esercitazione: Integrazione di Azure Active Directory con Workrite</span><span class="sxs-lookup"><span data-stu-id="72528-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="72528-104">Questa esercitazione descrive come integrare Workrite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72528-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72528-105">L'integrazione di Workrite con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="72528-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72528-106">È possibile controllare in Azure AD chi può accedere a Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="72528-107">È possibile abilitare gli utenti per l'accesso automatico a Workrite (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72528-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="72528-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72528-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="72528-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72528-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72528-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72528-110">Prerequisites</span></span>

<span data-ttu-id="72528-111">Per configurare l'integrazione di Azure AD con Workrite, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="72528-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="72528-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72528-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72528-113">Sottoscrizione di Workrite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="72528-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72528-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="72528-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72528-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="72528-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72528-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="72528-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72528-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72528-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72528-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="72528-118">Scenario description</span></span>
<span data-ttu-id="72528-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="72528-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72528-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="72528-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72528-121">Aggiunta di Workrite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="72528-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="72528-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72528-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="72528-123">Aggiunta di Workrite dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="72528-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="72528-124">Per configurare l'integrazione di Workrite in Azure AD, è necessario aggiungere Workrite dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="72528-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72528-125">**Per aggiungere Workrite dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="72528-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72528-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="72528-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="72528-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="72528-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72528-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="72528-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="72528-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="72528-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="72528-133">Nella casella di ricerca digitare **Workrite**, selezionare **Workrite** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72528-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite nell'elenco dei risultati](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="72528-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72528-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="72528-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workrite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="72528-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72528-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Workrite che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72528-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="72528-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="72528-139">Per stabilire la relazione di collegamento, in Workrite assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="72528-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="72528-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Workrite, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="72528-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72528-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="72528-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="72528-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72528-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72528-143">**[Creare un utente di test di Workrite](#create-a-workrite-test-user)** : per avere una controparte di Britta Simon in Workrite collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72528-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="72528-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72528-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72528-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="72528-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="72528-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72528-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="72528-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="72528-148">**Per configurare Single Sign-On di Azure AD con Workrite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="72528-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="72528-149">Nella pagina di integrazione dell'applicazione **Workrite** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="72528-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Configurare il collegamento Single Sign-On][4]

2. <span data-ttu-id="72528-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="72528-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="72528-153">Nella sezione **URL e dominio Workrite** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="72528-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="72528-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="72528-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72528-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="72528-156">This value is not real.</span></span> <span data-ttu-id="72528-157">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="72528-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="72528-158">Per ottenere questo valore, contattare il [team di supporto clienti di Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="72528-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="72528-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="72528-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="72528-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="72528-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72528-163">Nella sezione **Configurazione di Workrite** fare clic su **Configura Workrite** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="72528-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72528-164">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="72528-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="72528-166">Per configurare l'accesso Single Sign-On sul lato **Workrite** è necessario inviare il **certificato (Base64) scaricato e i valori Sign-Out URL (URL di disconnessione), SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** al [team di supporto Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="72528-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="72528-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="72528-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72528-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="72528-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72528-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72528-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="72528-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72528-170">Create an Azure AD test user</span></span>

<span data-ttu-id="72528-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72528-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="72528-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="72528-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72528-174">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="72528-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="72528-176">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="72528-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="72528-178">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="72528-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="72528-180">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="72528-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="72528-182">a.</span><span class="sxs-lookup"><span data-stu-id="72528-182">a.</span></span> <span data-ttu-id="72528-183">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72528-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72528-184">b.</span><span class="sxs-lookup"><span data-stu-id="72528-184">b.</span></span> <span data-ttu-id="72528-185">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72528-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="72528-186">c.</span><span class="sxs-lookup"><span data-stu-id="72528-186">c.</span></span> <span data-ttu-id="72528-187">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="72528-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="72528-188">d.</span><span class="sxs-lookup"><span data-stu-id="72528-188">d.</span></span> <span data-ttu-id="72528-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="72528-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="72528-190">Creare un utente test di Workrite</span><span class="sxs-lookup"><span data-stu-id="72528-190">Create a Workrite test user</span></span>

<span data-ttu-id="72528-191">Questa sezione descrive come creare un utente chiamato Britta Simon in Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="72528-192">**Per creare un utente test denominato Britta Simon in Workrite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="72528-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="72528-193">Accedere al sito aziendale di Workrite come amministratore.</span><span class="sxs-lookup"><span data-stu-id="72528-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="72528-194">Nel pannello di navigazione fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="72528-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Controllo Admin][400]

3. <span data-ttu-id="72528-196">Passare ai collegamenti rapidi e quindi fare clic su **Create a User** (Crea un utente).</span><span class="sxs-lookup"><span data-stu-id="72528-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Sezione Create a User (Crea un utente)][401]

4. <span data-ttu-id="72528-198">Nella finestra di dialogo **Create User** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="72528-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Finestra di dialogo Create User (Crea utente)][402]
    
    <span data-ttu-id="72528-200">a.</span><span class="sxs-lookup"><span data-stu-id="72528-200">a.</span></span> <span data-ttu-id="72528-201">Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="72528-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="72528-202">b.</span><span class="sxs-lookup"><span data-stu-id="72528-202">b.</span></span> <span data-ttu-id="72528-203">Digitare il nome dell'utente, ad esempio Britta, nella casella di testo **First Name** (Nome).</span><span class="sxs-lookup"><span data-stu-id="72528-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="72528-204">c.</span><span class="sxs-lookup"><span data-stu-id="72528-204">c.</span></span> <span data-ttu-id="72528-205">Digitare il cognome dell'utente, ad esempio Simon, nella casella di testo **Surname** (Cognome).</span><span class="sxs-lookup"><span data-stu-id="72528-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="72528-206">d.</span><span class="sxs-lookup"><span data-stu-id="72528-206">d.</span></span> <span data-ttu-id="72528-207">Selezionare **Client Administrator** in **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="72528-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="72528-208">e.</span><span class="sxs-lookup"><span data-stu-id="72528-208">e.</span></span> <span data-ttu-id="72528-209">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72528-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="72528-210">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72528-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="72528-211">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="72528-213">**Per assegnare Britta Simon a Workrite, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="72528-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="72528-214">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="72528-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="72528-216">Selezionare **Workrite**dall'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="72528-216">In the applications list, select **Workrite**.</span></span>

    ![Collegamento Workrite nell'elenco Applicazioni](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="72528-218">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="72528-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="72528-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72528-220">Click **Add** button.</span></span> <span data-ttu-id="72528-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="72528-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="72528-223">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="72528-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="72528-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="72528-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72528-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="72528-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="72528-226">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="72528-226">Test single sign-on</span></span>

<span data-ttu-id="72528-227">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="72528-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="72528-228">Quando si fa clic sul riquadro Workrite nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Workrite.</span><span class="sxs-lookup"><span data-stu-id="72528-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72528-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="72528-229">Additional resources</span></span>

* [<span data-ttu-id="72528-230">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72528-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72528-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72528-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

