---
title: 'Esercitazione: Integrazione di Azure Active Directory con Synergi | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Synergi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: dedbe96fbb26bc34c4d7e213892b318f0e6fef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="cb03d-103">Esercitazione: Integrazione di Azure Active Directory con Synergi</span><span class="sxs-lookup"><span data-stu-id="cb03d-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="cb03d-104">Questa esercitazione descrive come integrare Synergi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb03d-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb03d-105">L'integrazione di Synergi con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb03d-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb03d-106">È possibile controllare in Azure AD chi può accedere a Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="cb03d-107">È possibile abilitare gli utenti per l'accesso automatico a Synergi (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb03d-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cb03d-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb03d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cb03d-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb03d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb03d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb03d-110">Prerequisites</span></span>

<span data-ttu-id="cb03d-111">Per configurare l'integrazione di Azure AD con Synergi, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb03d-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="cb03d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb03d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb03d-113">Sottoscrizione di Synergi abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cb03d-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb03d-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cb03d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb03d-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb03d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb03d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cb03d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb03d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb03d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb03d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cb03d-118">Scenario description</span></span>
<span data-ttu-id="cb03d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cb03d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb03d-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb03d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb03d-121">Aggiunta di Synergi dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cb03d-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="cb03d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb03d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="cb03d-123">Aggiunta di Synergi dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cb03d-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="cb03d-124">Per configurare l'integrazione di Synergi in Azure AD, è necessario aggiungere Synergi dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cb03d-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb03d-125">**Per aggiungere Synergi dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cb03d-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb03d-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cb03d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="cb03d-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb03d-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="cb03d-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb03d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="cb03d-133">Nella casella di ricerca digitare **Synergi** selezionare **Synergi** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb03d-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi nell'elenco risultati](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cb03d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb03d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cb03d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Synergi in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cb03d-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb03d-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Synergi che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb03d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="cb03d-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="cb03d-139">Per stabilire la relazione di collegamento, in Synergi assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="cb03d-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb03d-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Synergi, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb03d-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb03d-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cb03d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb03d-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb03d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb03d-143">**[Creare un utente test di Synergi](#create-a-synergi-test-user)**: per avere una controparte di Britta Simon in Synergi collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb03d-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb03d-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb03d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb03d-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="cb03d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cb03d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb03d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cb03d-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="cb03d-148">**Per configurare l'accesso Single Sign-On di Azure AD con Synergi, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cb03d-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="cb03d-149">Nella pagina di integrazione dell'applicazione **Synergi** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="cb03d-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cb03d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="cb03d-153">Nella sezione **URL e dominio Synergi** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cb03d-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="cb03d-155">a.</span><span class="sxs-lookup"><span data-stu-id="cb03d-155">a.</span></span> <span data-ttu-id="cb03d-156">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="cb03d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="cb03d-157">b.</span><span class="sxs-lookup"><span data-stu-id="cb03d-157">b.</span></span> <span data-ttu-id="cb03d-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="cb03d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb03d-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="cb03d-159">These values are not real.</span></span> <span data-ttu-id="cb03d-160">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="cb03d-161">Per ottenere questi valori, contattare il [team di supporto di Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cb03d-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="cb03d-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="cb03d-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="cb03d-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cb03d-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb03d-166">Nella sezione **Configurazione di Synergi** fare clic su **Configura Synergi** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cb03d-167">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Entity ID (ID entità SAML)** dalla **sezione Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="cb03d-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurazione di Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="cb03d-169">Per configurare l'accesso Single Sign-On sul lato **Synergi**, è necessario inviare i valori scaricati per **Certificate(Base64), Sign-Out URL, and SAML Entity ID** (Certificato - Base64, URL di disconnessione e ID entità SAML) al [team di supporto di Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cb03d-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="cb03d-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="cb03d-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb03d-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="cb03d-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb03d-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb03d-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cb03d-173">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb03d-173">Create an Azure AD test user</span></span>

<span data-ttu-id="cb03d-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb03d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="cb03d-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cb03d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb03d-177">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="cb03d-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cb03d-179">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cb03d-181">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cb03d-183">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cb03d-183">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cb03d-185">a.</span><span class="sxs-lookup"><span data-stu-id="cb03d-185">a.</span></span> <span data-ttu-id="cb03d-186">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb03d-187">b.</span><span class="sxs-lookup"><span data-stu-id="cb03d-187">b.</span></span> <span data-ttu-id="cb03d-188">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb03d-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cb03d-189">c.</span><span class="sxs-lookup"><span data-stu-id="cb03d-189">c.</span></span> <span data-ttu-id="cb03d-190">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cb03d-191">d.</span><span class="sxs-lookup"><span data-stu-id="cb03d-191">d.</span></span> <span data-ttu-id="cb03d-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="cb03d-193">Creare un utente test di Synergi</span><span class="sxs-lookup"><span data-stu-id="cb03d-193">Create a Synergi test user</span></span>

<span data-ttu-id="cb03d-194">In questa sezione viene creato un utente chiamato Britta Simon in Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="cb03d-195">Collaborare con il [team di supporto di Synergi](https://www.irmsecurity.com/contact/) per aggiungere gli utenti alla piattaforma Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="cb03d-196">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cb03d-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cb03d-197">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb03d-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="cb03d-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="cb03d-200">**Per assegnare Britta Simon a Synergi, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cb03d-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="cb03d-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cb03d-203">Nell'elenco di applicazioni, selezionare **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-203">In the applications list, select **Synergi**.</span></span>

    ![Collegamento di Synergi nell'elenco delle applicazioni](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="cb03d-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="cb03d-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="cb03d-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-207">Click **Add** button.</span></span> <span data-ttu-id="cb03d-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="cb03d-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="cb03d-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb03d-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb03d-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cb03d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cb03d-213">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cb03d-213">Test single sign-on</span></span>

<span data-ttu-id="cb03d-214">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cb03d-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cb03d-215">Quando si fa clic sul riquadro Synergi nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Synergi.</span><span class="sxs-lookup"><span data-stu-id="cb03d-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="cb03d-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb03d-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb03d-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cb03d-217">Additional resources</span></span>

* [<span data-ttu-id="cb03d-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb03d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb03d-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb03d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

