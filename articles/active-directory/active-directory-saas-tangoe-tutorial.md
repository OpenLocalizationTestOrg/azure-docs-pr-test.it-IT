---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tangoe Command Premium Mobile | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Tangoe Command Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="8b2cd-103">Esercitazione: Integrazione di Azure Active Directory con Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="8b2cd-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="8b2cd-104">Questa esercitazione descrive come integrare Tangoe Command Premium Mobile con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b2cd-105">L'integrazione di Tangoe Command Premium Mobile con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b2cd-106">È possibile controllare in Azure AD chi può accedere a Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="8b2cd-107">È possibile abilitare gli utenti per l'accesso automatico a Tangoe Command Premium Mobile (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b2cd-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b2cd-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b2cd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b2cd-110">Prerequisites</span></span>

<span data-ttu-id="8b2cd-111">Per configurare l'integrazione di Azure AD con Tangoe Command Premium Mobile, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="8b2cd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b2cd-113">Sottoscrizione di Tangoe Command Premium Mobile abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b2cd-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b2cd-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b2cd-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b2cd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b2cd-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b2cd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8b2cd-118">Scenario description</span></span>
<span data-ttu-id="8b2cd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b2cd-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b2cd-121">Aggiungere Tangoe Command Premium Mobile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8b2cd-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="8b2cd-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="8b2cd-123">Aggiungere Tangoe Command Premium Mobile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8b2cd-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="8b2cd-124">Per configurare l'integrazione di Tangoe Command Premium Mobile in Azure AD, è necessario aggiungere Tangoe Command Premium Mobile dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b2cd-125">**Per aggiungere Tangoe Command Premium Mobile dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b2cd-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b2cd-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b2cd-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8b2cd-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8b2cd-133">Nella casella di ricerca digitare **Tangoe Command Premium Mobile**, selezionare **Tangoe Command Premium Mobile** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="8b2cd-134">Aggiungere Tangoe Command Premium Mobile dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="8b2cd-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8b2cd-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8b2cd-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tangoe Command Premium Mobile con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8b2cd-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b2cd-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Tangoe Command Premium Mobile che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="8b2cd-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="8b2cd-139">Per stabilire la relazione di collegamento, in Tangoe Command Premium Mobile assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b2cd-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Tangoe Command Premium Mobile, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b2cd-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b2cd-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b2cd-143">**[Creare un utente di test di Tangoe Command Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**: per avere una controparte di Britta Simon in Tangoe Command Premium Mobile collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b2cd-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b2cd-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8b2cd-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8b2cd-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="8b2cd-148">**Per configurare Single Sign-On di Azure AD con Tangoe Command Premium Mobile, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="8b2cd-149">Nella pagina di integrazione dell'applicazione **Tangoe Command Premium Mobile** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8b2cd-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="8b2cd-153">Nella sezione **URL e dominio Tangoe Command Premium Mobile** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![URL e dominio Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="8b2cd-155">a.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-155">a.</span></span> <span data-ttu-id="8b2cd-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="8b2cd-157">b.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-157">b.</span></span> <span data-ttu-id="8b2cd-158">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="8b2cd-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b2cd-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="8b2cd-159">These values are not real.</span></span> <span data-ttu-id="8b2cd-160">Aggiornare questi valori con URL di risposta e URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8b2cd-161">Per ottenere questi valori, contattare il [team di supporto clienti di Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="8b2cd-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="8b2cd-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8b2cd-164">Click **Save** button.</span></span>

    ![Pulsante per il salvataggio](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="8b2cd-166">Nella sezione **Configurazione di Tangoe Command Premium Mobile** fare clic su **Configura Tangoe Command Premium Mobile** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8b2cd-167">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sezione di configurazione di Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="8b2cd-169">Per configurare l'accesso SSO per l'applicazione, contattare il [team di supporto clienti di Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) e fornire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="8b2cd-170">Il file dei metadati scaricato</span><span class="sxs-lookup"><span data-stu-id="8b2cd-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="8b2cd-171">**ID di entità SAML**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="8b2cd-172">**URL del servizio Single Sign-On SAML**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="8b2cd-173">**URL di disconnessione**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="8b2cd-174">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b2cd-175">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b2cd-176">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8b2cd-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-177">Create an Azure AD test user</span></span>
<span data-ttu-id="8b2cd-178">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8b2cd-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b2cd-181">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b2cd-183">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utenti e gruppi -> Tutti gli utenti](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b2cd-185">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add user](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b2cd-187">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8b2cd-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Finestra di dialogo Utente](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b2cd-189">a.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-189">a.</span></span> <span data-ttu-id="8b2cd-190">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b2cd-191">b.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-191">b.</span></span> <span data-ttu-id="8b2cd-192">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b2cd-193">c.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-193">c.</span></span> <span data-ttu-id="8b2cd-194">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b2cd-195">d.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-195">d.</span></span> <span data-ttu-id="8b2cd-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="8b2cd-197">Creare un utente di test di Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="8b2cd-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="8b2cd-198">In questa sezione viene creato un utente chiamato Britta Simon in Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="8b2cd-199">L'applicazione Tangoe Command Premium Mobile richiede che venga effettuato il provisioning di tutti gli utenti all'interno dell'applicazione prima di eseguire l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="8b2cd-200">Collaborare con il [team di supporto clienti di Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) per effettuare il provisioning di tutti gli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8b2cd-201">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b2cd-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="8b2cd-202">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8b2cd-204">**Per assegnare Britta Simon a Tangoe Command Premium Mobile, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8b2cd-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="8b2cd-205">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8b2cd-207">Nell'elenco delle applicazioni selezionare **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile nell'elenco delle app](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="8b2cd-209">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8b2cd-211">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-211">Click **Add** button.</span></span> <span data-ttu-id="8b2cd-212">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8b2cd-214">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b2cd-215">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b2cd-216">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8b2cd-217">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8b2cd-217">Test single sign-on</span></span>

<span data-ttu-id="8b2cd-218">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8b2cd-219">Quando si fa clic sul riquadro Tangoe Command Premium Mobile nel pannello di accesso, viene effettuato automaticamente l'accesso all'applicazione Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="8b2cd-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="8b2cd-220">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b2cd-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8b2cd-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8b2cd-221">Additional resources</span></span>

* [<span data-ttu-id="8b2cd-222">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b2cd-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b2cd-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b2cd-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

