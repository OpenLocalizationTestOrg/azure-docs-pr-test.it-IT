---
title: 'Esercitazione: Integrazione di Azure Active Directory con Yonyx Interactive Guides | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Yonyx Interactive Guides.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 522f440a0b3746e1101aed845678b3930e030fec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="1f3b7-103">Esercitazione: Integrazione di Azure Active Directory con Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="1f3b7-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="1f3b7-104">Questa esercitazione descrive come integrare Yonyx Interactive Guides con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f3b7-105">L'integrazione di Yonyx Interactive Guides con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f3b7-106">È possibile controllare in Azure AD chi può accedere a Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="1f3b7-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
- <span data-ttu-id="1f3b7-107">È possibile abilitare gli utenti per l'accesso automatico a Yonyx Interactive Guides (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f3b7-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f3b7-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f3b7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1f3b7-110">Prerequisites</span></span>

<span data-ttu-id="1f3b7-111">Per configurare l'integrazione di Azure AD con Yonyx Interactive Guides, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

- <span data-ttu-id="1f3b7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f3b7-113">Sottoscrizione di Yonyx Interactive Guides abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1f3b7-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f3b7-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f3b7-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f3b7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f3b7-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f3b7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1f3b7-118">Scenario description</span></span>
<span data-ttu-id="1f3b7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f3b7-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f3b7-121">Aggiunta di Yonyx Interactive Guides dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1f3b7-121">Adding Yonyx Interactive Guides from the gallery</span></span>
2. <span data-ttu-id="1f3b7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="1f3b7-123">Aggiunta di Yonyx Interactive Guides dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1f3b7-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="1f3b7-124">Per configurare l'integrazione di Yonyx Interactive Guides in Azure AD, è necessario aggiungere Yonyx Interactive Guides dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f3b7-125">**Per aggiungere Yonyx Interactive Guides dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f3b7-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f3b7-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="1f3b7-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f3b7-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="1f3b7-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="1f3b7-133">Nella casella di ricerca digitare **Yonyx Interactive Guides**, selezionare **Yonyx Interactive Guides** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span></span>

    ![Yonyx Interactive Guides nell'elenco dei risultati](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1f3b7-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1f3b7-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Yonyx Interactive Guides in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1f3b7-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f3b7-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Yonyx Interactive Guides che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span></span> <span data-ttu-id="1f3b7-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="1f3b7-139">Per stabilire la relazione di collegamento, in Yonyx Interactive Guides assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1f3b7-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Yonyx Interactive Guides, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f3b7-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f3b7-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f3b7-143">**[Creare un utente di test di Yonyx Interactive Guides](#create-a-yonyx-interactive-guides-test-user)** : per avere una controparte di Britta Simon in Yonyx Interactive Guides collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f3b7-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f3b7-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1f3b7-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1f3b7-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="1f3b7-148">**Per configurare l'accesso Single Sign-On di Azure AD con Yonyx Interactive Guides, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f3b7-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="1f3b7-149">Nella pagina di integrazione dell'applicazione **Yonyx Interactive Guides** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Configurare il collegamento Single Sign-On][4]

2. <span data-ttu-id="1f3b7-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="1f3b7-153">Nella sezione **URL e dominio Yonyx Interactive Guides** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="1f3b7-155">a.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-155">a.</span></span> <span data-ttu-id="1f3b7-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="1f3b7-157">b.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-157">b.</span></span> <span data-ttu-id="1f3b7-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="1f3b7-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f3b7-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1f3b7-159">These values are not real.</span></span> <span data-ttu-id="1f3b7-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1f3b7-161">Per ottenere questi valori, contattare il [team di supporto clienti di Yonyx Interactive Guides](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1f3b7-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="1f3b7-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1f3b7-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f3b7-166">Nella sezione **Configurazione di Yonyx Interactive Guides** fare clic su **Configura Yonyx Interactive Guides** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f3b7-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1f3b7-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="1f3b7-169">Per configurare l'accesso Single Sign-On sul lato **Yonyx Interactive Guides**, è necessario inviare il **certificato (Base64)** scaricato e i valori **URL di disconnessione**, **URL del servizio Single Sign-On SAML** e **ID entità SAML** al [team di supporto di Yonyx Interactive Guides](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="1f3b7-170">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1f3b7-171">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f3b7-172">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f3b7-173">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1f3b7-174">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-174">Create an Azure AD test user</span></span>

<span data-ttu-id="1f3b7-175">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

  ![Creare un utente test di Azure AD][100]

<span data-ttu-id="1f3b7-177">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1f3b7-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f3b7-178">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f3b7-180">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f3b7-182">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Pulsante Aggiungi](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f3b7-184">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1f3b7-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f3b7-186">a.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-186">a.</span></span> <span data-ttu-id="1f3b7-187">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f3b7-188">b.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-188">b.</span></span> <span data-ttu-id="1f3b7-189">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f3b7-190">c.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-190">c.</span></span> <span data-ttu-id="1f3b7-191">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f3b7-192">d.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-192">d.</span></span> <span data-ttu-id="1f3b7-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="1f3b7-194">Creare un utente test di Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="1f3b7-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="1f3b7-195">Questa sezione descrive come creare un utente chiamato Britta Simon in Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="1f3b7-196">Yonyx Interactive Guides supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1f3b7-197">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-197">There is no action item for you in this section.</span></span> <span data-ttu-id="1f3b7-198">Durante un tentativo di accesso a Yonyx Interactive Guides viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1f3b7-199">Per creare un utente manualmente è necessario contattare il team di supporto di Yonyx Interactive Guides all'indirizzo <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1f3b7-200">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f3b7-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="1f3b7-201">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span></span>

![Assegnare il ruolo utente][200]

<span data-ttu-id="1f3b7-203">**Per assegnare Britta Simon a Yonyx Interactive Guides, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1f3b7-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="1f3b7-204">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1f3b7-206">Nell'elenco delle applicazioni selezionare **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-206">In the applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Collegamento a Yonyx Interactive Guides nell'elenco delle applicazioni](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="1f3b7-208">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="1f3b7-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-210">Click **Add** button.</span></span> <span data-ttu-id="1f3b7-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="1f3b7-213">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f3b7-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f3b7-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1f3b7-216">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1f3b7-216">Test single sign-on</span></span>

<span data-ttu-id="1f3b7-217">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f3b7-218">Quando si fa clic sul riquadro Yonyx Interactive Guides nel pannello di accesso, si accederà automaticamente all'applicazione Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1f3b7-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="1f3b7-219">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f3b7-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f3b7-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1f3b7-220">Additional resources</span></span>

* [<span data-ttu-id="1f3b7-221">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f3b7-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f3b7-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f3b7-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

