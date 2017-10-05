---
title: 'Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="d3303-103">Esercitazione: Integrazione di Azure Active Directory con TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="d3303-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="d3303-104">Questa esercitazione descrive come integrare TINFOIL SECURITY con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3303-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3303-105">L'integrazione di TINFOIL SECURITY con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3303-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3303-106">È possibile controllare in Azure AD chi può accedere a TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="d3303-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="d3303-107">È possibile abilitare gli utenti per l'accesso automatico a TINFOIL SECURITY (Single Sign-On) con gli account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3303-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3303-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3303-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3303-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3303-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3303-110">Prerequisites</span></span>

<span data-ttu-id="d3303-111">Per configurare l'integrazione di Azure AD con TINFOIL SECURITY, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3303-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="d3303-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3303-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3303-113">Sottoscrizione di TINFOIL SECURITY abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3303-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3303-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d3303-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3303-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3303-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3303-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d3303-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3303-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3303-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3303-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d3303-118">Scenario description</span></span>
<span data-ttu-id="d3303-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d3303-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3303-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3303-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3303-121">Aggiungere TINFOIL SECURITY dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d3303-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="d3303-122">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="d3303-123">Aggiungere TINFOIL SECURITY dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d3303-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="d3303-124">Per configurare l'integrazione di TINFOIL SECURITY in Azure AD, è necessario aggiungere TINFOIL SECURITY dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d3303-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3303-125">**Per aggiungere TINFOIL SECURITY dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3303-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3303-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d3303-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3303-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d3303-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3303-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3303-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d3303-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3303-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d3303-133">Nella casella di ricerca digitare **TINFOIL SECURITY**, selezionare **TINFOIL SECURITY** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3303-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![TINFOIL SECURITY dalla raccolta](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3303-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d3303-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TINFOIL SECURITY con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3303-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3303-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve individuare l'utente di TINFOIL SECURITY corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3303-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="d3303-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="d3303-139">Per stabilire la relazione di collegamento, in TINFOIL SECURITY assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="d3303-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3303-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con TINFOIL SECURITY, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3303-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3303-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d3303-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3303-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3303-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3303-143">**[Creazione di un utente test di TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**: per avere una controparte di Britta Simon in TINFOIL SECURITY collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d3303-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3303-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3303-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3303-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d3303-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3303-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d3303-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="d3303-148">**Per configurare l'accesso Single Sign-On di Azure AD con TINFOIL SECURITY, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3303-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="d3303-149">Nella pagina di integrazione dell'applicazione **TINFOIL SECURITY** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d3303-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d3303-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d3303-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Accesso basato su SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="d3303-153">Nella sezione **URL e dominio TINFOIL SECURITY** l'utente non deve eseguire alcuna operazione poiché l'app è già integrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3303-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="d3303-155">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE**.</span><span class="sxs-lookup"><span data-stu-id="d3303-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![Sezione Certificato di firma SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="d3303-157">Per aggiungere i mapping di attributi obbligatori, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d3303-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="d3303-158">![Attributi](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="d3303-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="d3303-159">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="d3303-159">Attribute Name</span></span>    |   <span data-ttu-id="d3303-160">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="d3303-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="d3303-161">accountid</span><span class="sxs-lookup"><span data-stu-id="d3303-161">accountid</span></span> | <span data-ttu-id="d3303-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="d3303-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="d3303-163">a.</span><span class="sxs-lookup"><span data-stu-id="d3303-163">a.</span></span> <span data-ttu-id="d3303-164">Fare clic su **Aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="d3303-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="d3303-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="d3303-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="d3303-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="d3303-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="d3303-167">b.</span><span class="sxs-lookup"><span data-stu-id="d3303-167">b.</span></span> <span data-ttu-id="d3303-168">Nella casella di testo **Nome attributo**, digitare **accountid**.</span><span class="sxs-lookup"><span data-stu-id="d3303-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="d3303-169">c.</span><span class="sxs-lookup"><span data-stu-id="d3303-169">c.</span></span> <span data-ttu-id="d3303-170">Nella casella di testo **Valore attributo** incollare il valore di ID account ottenuto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d3303-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="d3303-171">d.</span><span class="sxs-lookup"><span data-stu-id="d3303-171">d.</span></span> <span data-ttu-id="d3303-172">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3303-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="d3303-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d3303-173">Click **Save** button.</span></span>

    ![Pulsante Salva](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d3303-175">Nella sezione **Configurazione di TINFOIL SECURITY** fare clic su **Configura TINFOIL SECURITY** per visualizzare la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d3303-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3303-176">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d3303-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="d3303-178">In un'altra finestra del Web browser accedere al sito aziendale TINFOIL SECURITY come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d3303-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="d3303-179">Nel barra degli strumenti in alto fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="d3303-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="d3303-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="d3303-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="d3303-181">Fare clic su **Security**.</span><span class="sxs-lookup"><span data-stu-id="d3303-181">Click **Security**.</span></span>
   
    <span data-ttu-id="d3303-182">![Sicurezza](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Sicurezza")</span><span class="sxs-lookup"><span data-stu-id="d3303-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="d3303-183">Nella pagina di configurazione **Single Sign-On** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d3303-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="d3303-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d3303-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="d3303-185">a.</span><span class="sxs-lookup"><span data-stu-id="d3303-185">a.</span></span> <span data-ttu-id="d3303-186">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="d3303-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="d3303-187">b.</span><span class="sxs-lookup"><span data-stu-id="d3303-187">b.</span></span> <span data-ttu-id="d3303-188">Fare clic su **Configurazione manuale**.</span><span class="sxs-lookup"><span data-stu-id="d3303-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="d3303-189">c.</span><span class="sxs-lookup"><span data-stu-id="d3303-189">c.</span></span> <span data-ttu-id="d3303-190">Nella casella di testo **SAML Post URL** (URL post SAML) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d3303-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="d3303-191">d.</span><span class="sxs-lookup"><span data-stu-id="d3303-191">d.</span></span> <span data-ttu-id="d3303-192">Nella casella di testo **SAML Certificate Fingerprint** (Impronta digitale certificato SAML) incollare il valore di **Identificazione personale** copiato dalla sezione **Certificato di firma SAML**.</span><span class="sxs-lookup"><span data-stu-id="d3303-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="d3303-193">e.</span><span class="sxs-lookup"><span data-stu-id="d3303-193">e.</span></span> <span data-ttu-id="d3303-194">Copiare il valore **Your Account ID** (ID account) e incollarlo nella casella di testo **Valore attributo** nella sezione **Aggiungi attributo** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3303-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="d3303-195">f.</span><span class="sxs-lookup"><span data-stu-id="d3303-195">f.</span></span> <span data-ttu-id="d3303-196">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="d3303-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d3303-197">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d3303-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3303-198">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d3303-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3303-199">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3303-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3303-200">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-200">Create an Azure AD test user</span></span>
<span data-ttu-id="d3303-201">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3303-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d3303-203">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3303-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3303-204">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d3303-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3303-206">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d3303-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="d3303-207">Utenti e gruppi -> Tutti gli utenti</span><span class="sxs-lookup"><span data-stu-id="d3303-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3303-208">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d3303-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Utente](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3303-210">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d3303-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3303-212">a.</span><span class="sxs-lookup"><span data-stu-id="d3303-212">a.</span></span> <span data-ttu-id="d3303-213">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3303-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3303-214">b.</span><span class="sxs-lookup"><span data-stu-id="d3303-214">b.</span></span> <span data-ttu-id="d3303-215">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3303-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3303-216">c.</span><span class="sxs-lookup"><span data-stu-id="d3303-216">c.</span></span> <span data-ttu-id="d3303-217">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d3303-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3303-218">d.</span><span class="sxs-lookup"><span data-stu-id="d3303-218">d.</span></span> <span data-ttu-id="d3303-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d3303-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="d3303-220">Creare un utente test di TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="d3303-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="d3303-221">Per consentire agli utenti di Azure AD di accedere a TINFOIL SECURITY, è necessario eseguirne il provisioning in TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="d3303-222">In TINFOIL SECURITY il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d3303-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="d3303-223">**Per eseguire il provisioning di un utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3303-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="d3303-224">Se l'utente fa parte di un account aziendale, è necessario [contattare il team di supporto TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) per creare l'account utente.</span><span class="sxs-lookup"><span data-stu-id="d3303-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="d3303-225">Se l'utente è un normale utente SaaS TINFOIL SECURITY, può aggiungere un collaboratore a uno qualsiasi dei siti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d3303-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="d3303-226">Viene attivato un processo per l'invio all'indirizzo di posta elettronica specificato di un invito a creare un nuovo account utente di TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="d3303-227">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerta da TINFOIL SECURITY per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3303-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3303-228">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3303-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="d3303-229">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d3303-231">**Per assegnare Britta Simon a TINFOIL SECURITY, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d3303-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="d3303-232">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3303-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d3303-234">Nell'elenco di applicazioni selezionare **TINFOIL SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="d3303-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![selezionare TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="d3303-236">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d3303-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d3303-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d3303-238">Click **Add** button.</span></span> <span data-ttu-id="d3303-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3303-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d3303-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d3303-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3303-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d3303-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3303-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3303-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d3303-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3303-244">Test single sign-on</span></span>

<span data-ttu-id="d3303-245">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d3303-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3303-246">Quando si fa clic sul riquadro TINFOIL SECURITY nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TINFOIL SECURITY.</span><span class="sxs-lookup"><span data-stu-id="d3303-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="d3303-247">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3303-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3303-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d3303-248">Additional resources</span></span>

* [<span data-ttu-id="d3303-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3303-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3303-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3303-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

