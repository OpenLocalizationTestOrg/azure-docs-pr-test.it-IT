---
title: 'Esercitazione: Integrazione di Azure Active Directory con Fuse | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Fuse.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9a91e22faced9e126043bebefd85c307dbdf933d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="270e5-103">Esercitazione: Integrazione di Azure Active Directory con Fuse</span><span class="sxs-lookup"><span data-stu-id="270e5-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="270e5-104">Questa esercitazione descrive come integrare Fuse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="270e5-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="270e5-105">L'integrazione di Fuse con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="270e5-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="270e5-106">È possibile controllare in Azure AD chi può accedere a Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="270e5-107">È possibile abilitare gli utenti per l'accesso automatico a Fuse (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="270e5-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="270e5-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="270e5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="270e5-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="270e5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="270e5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="270e5-110">Prerequisites</span></span>

<span data-ttu-id="270e5-111">Per configurare l'integrazione di Azure AD con Fuse, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="270e5-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="270e5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="270e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="270e5-113">Sottoscrizione di Fuse abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="270e5-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="270e5-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="270e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="270e5-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="270e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="270e5-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="270e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="270e5-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="270e5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="270e5-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="270e5-118">Scenario description</span></span>
<span data-ttu-id="270e5-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="270e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="270e5-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="270e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="270e5-121">Aggiungere Fuse dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="270e5-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="270e5-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="270e5-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="270e5-123">Aggiungere Fuse dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="270e5-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="270e5-124">Per configurare l'integrazione di Fuse in Azure AD, è necessario aggiungere Fuse dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="270e5-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="270e5-125">**Per aggiungere Fuse dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="270e5-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="270e5-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="270e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="270e5-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="270e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="270e5-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="270e5-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="270e5-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="270e5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="270e5-133">Nella casella di ricerca digitare **Fuse**, selezionare **Fuse** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="270e5-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Fuse nell'elenco risultati](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="270e5-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="270e5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="270e5-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Fuse in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="270e5-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="270e5-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Fuse che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="270e5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="270e5-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="270e5-139">Per stabilire la relazione di collegamento, in Fuse assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="270e5-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="270e5-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Fuse, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="270e5-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="270e5-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="270e5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="270e5-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="270e5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="270e5-143">**[Creare un utente di test di Fuse](#create-a-fuse-test-user)**: per avere una controparte di Britta Simon in Fuse collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="270e5-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="270e5-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="270e5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="270e5-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="270e5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="270e5-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="270e5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="270e5-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="270e5-148">**Per configurare Single Sign-On di Azure AD con Fuse, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="270e5-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="270e5-149">Nella pagina di integrazione dell'applicazione **Fuse** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="270e5-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="270e5-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="270e5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="270e5-153">Nella sezione **URL e dominio Fuse** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="270e5-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="270e5-155">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant name>.fusion-universal.com/`.</span><span class="sxs-lookup"><span data-stu-id="270e5-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="270e5-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="270e5-156">This value is not real.</span></span> <span data-ttu-id="270e5-157">è necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="270e5-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="270e5-158">Per ottenere questo valore, contattare il [team di supporto clienti di Fuse](mailto:support@fusion-universal.com).</span><span class="sxs-lookup"><span data-stu-id="270e5-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="270e5-159">Nella sezione **Certificato di firma SAML** fare clic su **Certificate (Raw)** (Certificato (base)) e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="270e5-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="270e5-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="270e5-161">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="270e5-163">Nella sezione **Configurazione di Fuse** fare clic su **Configura Fuse** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="270e5-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="270e5-164">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="270e5-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="270e5-166">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il [team di supporto di Fuse](mailto:support@fusion-universal.com) e fornire i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="270e5-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="270e5-167">**File del certificato (base)** scaricato</span><span class="sxs-lookup"><span data-stu-id="270e5-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="270e5-168">**URL del servizio Single Sign-On SAML**</span><span class="sxs-lookup"><span data-stu-id="270e5-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="270e5-169">**ID di entità SAML**</span><span class="sxs-lookup"><span data-stu-id="270e5-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="270e5-170">**URL di disconnessione**</span><span class="sxs-lookup"><span data-stu-id="270e5-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="270e5-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="270e5-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="270e5-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="270e5-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="270e5-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="270e5-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="270e5-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="270e5-174">Create an Azure AD test user</span></span>

<span data-ttu-id="270e5-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="270e5-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="270e5-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="270e5-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="270e5-178">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="270e5-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="270e5-180">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="270e5-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="270e5-182">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="270e5-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="270e5-184">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="270e5-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="270e5-186">a.</span><span class="sxs-lookup"><span data-stu-id="270e5-186">a.</span></span> <span data-ttu-id="270e5-187">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="270e5-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="270e5-188">b.</span><span class="sxs-lookup"><span data-stu-id="270e5-188">b.</span></span> <span data-ttu-id="270e5-189">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="270e5-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="270e5-190">c.</span><span class="sxs-lookup"><span data-stu-id="270e5-190">c.</span></span> <span data-ttu-id="270e5-191">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="270e5-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="270e5-192">d.</span><span class="sxs-lookup"><span data-stu-id="270e5-192">d.</span></span> <span data-ttu-id="270e5-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="270e5-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="270e5-194">Creare un utente test di Fuse</span><span class="sxs-lookup"><span data-stu-id="270e5-194">Create a Fuse test user</span></span>

<span data-ttu-id="270e5-195">In questa sezione viene creato un utente di nome Britta Simon in Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="270e5-196">Collaborare con il [team di supporto di Fuse](mailto:support@fusion-universal.com) per aggiungere gli utenti alla piattaforma Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="270e5-197">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="270e5-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="270e5-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="270e5-200">**Per assegnare Britta Simon a Fuse, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="270e5-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="270e5-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="270e5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="270e5-203">Nell'elenco delle applicazioni selezionare **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="270e5-203">In the applications list, select **Fuse**.</span></span>

    ![Collegamento di Fuse nell'elenco delle applicazioni](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="270e5-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="270e5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="270e5-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="270e5-207">Click **Add** button.</span></span> <span data-ttu-id="270e5-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="270e5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="270e5-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="270e5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="270e5-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="270e5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="270e5-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="270e5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="270e5-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="270e5-213">Test single sign-on</span></span>

<span data-ttu-id="270e5-214">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="270e5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="270e5-215">Quando si fa clic sul riquadro Fuse nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Fuse.</span><span class="sxs-lookup"><span data-stu-id="270e5-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="270e5-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="270e5-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="270e5-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="270e5-217">Additional resources</span></span>

* [<span data-ttu-id="270e5-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="270e5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="270e5-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="270e5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

