---
title: 'Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS) | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Amazon Web Services.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="f0799-103">Esercitazione: Integrazione di Azure Active Directory con Amazon Web Service (AWS)</span><span class="sxs-lookup"><span data-stu-id="f0799-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="f0799-104">Questa esercitazione descrive come integrare Amazon Web Services (AWS) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0799-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0799-105">L'integrazione di Amazon Web Service (AWS) con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0799-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0799-106">è possibile controllare in Azure AD chi può accedere ad Amazon Web Service (AWS)</span><span class="sxs-lookup"><span data-stu-id="f0799-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="f0799-107">è possibile abilitare gli utenti per l'accesso automatico ad Amazon Web Service (AWS) (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0799-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f0799-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0799-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0799-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="f0799-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f0799-110">Prerequisites</span></span>

<span data-ttu-id="f0799-111">Per configurare l'integrazione di Azure AD con Amazon Web Service (AWS), sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0799-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="f0799-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0799-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0799-113">Sottoscrizione Amazon Web Service (AWS) abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f0799-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0799-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0799-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0799-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0799-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f0799-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f0799-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0799-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0799-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f0799-118">Scenario description</span></span>
<span data-ttu-id="f0799-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f0799-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0799-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0799-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0799-121">Aggiunta di Amazon Web Service (AWS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f0799-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="f0799-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="f0799-123">Aggiunta di Amazon Web Service (AWS) dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="f0799-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="f0799-124">Per configurare l'integrazione di Amazon Web Service (AWS) in Azure AD, è necessario aggiungere Amazon Web Service (AWS) dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f0799-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0799-125">**Per aggiungere Amazon Web Service (AWS) dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f0799-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0799-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f0799-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0799-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f0799-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0799-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f0799-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f0799-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f0799-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f0799-133">Nella casella di ricerca digitare **Amazon Web Service (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="f0799-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="f0799-135">Nel riquadro dei risultati selezionare **Amazon Web Service (AWS)** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0799-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0799-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Amazon Web Services (AWS) usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f0799-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0799-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Amazon Web Service (AWS) che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0799-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="f0799-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l’utente correlato in Amazon Web Service (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="f0799-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **NomeUtente** in Amazon Web Service (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="f0799-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Amazon Web Service (AWS), è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0799-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0799-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f0799-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0799-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0799-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0799-145">**[Creazione di un utente test in Amazon Web Service](#creating-an-amazon-web-services-test-user)**: per avere una controparte di Britta Simon in Amazon Web Service (AWS) collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0799-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f0799-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0799-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0799-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="f0799-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0799-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0799-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="f0799-150">**Per configurare l'accesso Single Sign-On di Azure AD con Amazon Web Service (AWS), seguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0799-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="f0799-151">Nella pagina di integrazione dell'applicazione **Amazon Web Services (AWS)** del Portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f0799-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f0799-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f0799-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="f0799-155">Nella sezione **URL e dominio Amazon Web Services (AWS)** l'utente non deve eseguire alcuna operazione perché l'applicazione è già preintegrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0799-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="f0799-157">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="f0799-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="f0799-159">L'applicazione Amazon Web Services (AWS) si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="f0799-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f0799-160">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="f0799-161">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f0799-162">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-162">The following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="f0799-164">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f0799-165">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="f0799-165">Attribute Name</span></span>  | <span data-ttu-id="f0799-166">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="f0799-166">Attribute Value</span></span> | <span data-ttu-id="f0799-167">Spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="f0799-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="f0799-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="f0799-168">RoleSessionName</span></span> | <span data-ttu-id="f0799-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f0799-169">user.userprincipalname</span></span> | <span data-ttu-id="f0799-170">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="f0799-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="f0799-171">Ruolo</span><span class="sxs-lookup"><span data-stu-id="f0799-171">Role</span></span>            | <span data-ttu-id="f0799-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="f0799-172">user.assignedroles</span></span> |  <span data-ttu-id="f0799-173">https://AWS.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="f0799-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="f0799-174">È necessario configurare il provisioning dell'utente in Azure AD per recuperare tutti i ruoli dalla Console AWS.</span><span class="sxs-lookup"><span data-stu-id="f0799-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="f0799-175">Consultare le seguente procedura di provisioning.</span><span class="sxs-lookup"><span data-stu-id="f0799-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="f0799-176">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-176">a.</span></span> <span data-ttu-id="f0799-177">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="f0799-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="f0799-179">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-179">b.</span></span> <span data-ttu-id="f0799-180">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="f0799-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f0799-182">c.</span><span class="sxs-lookup"><span data-stu-id="f0799-182">c.</span></span> <span data-ttu-id="f0799-183">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="f0799-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="f0799-184">Aggiungere il valore di Namespace come indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f0799-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="f0799-185">d.</span><span class="sxs-lookup"><span data-stu-id="f0799-185">d.</span></span> <span data-ttu-id="f0799-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0799-186">Click **Ok**.</span></span>

7. <span data-ttu-id="f0799-187">Fare clic sul pulsante **Salva** per salvare le impostazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="f0799-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f0799-189">In un'altra finestra del Web browser accedere al sito aziendale di Amazon Web Service (AWS) come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f0799-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="f0799-190">Fare clic su **Console Home**.</span><span class="sxs-lookup"><span data-stu-id="f0799-190">Click **Console Home**.</span></span>
   
    ![Configura accesso Single Sign-On][11]

10. <span data-ttu-id="f0799-192">Fare clic su **IAM** dal servizio **Sicurezza, identità e conformità**.</span><span class="sxs-lookup"><span data-stu-id="f0799-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Configura accesso Single Sign-On][12]

11. <span data-ttu-id="f0799-194">Fare clic su **Provider di identità** e quindi fare clic su **Create Provider** (Crea provider).</span><span class="sxs-lookup"><span data-stu-id="f0799-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Configura accesso Single Sign-On][13]

12. <span data-ttu-id="f0799-196">Nella pagina **Configure Provider** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On][14]
 
    <span data-ttu-id="f0799-198">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-198">a.</span></span> <span data-ttu-id="f0799-199">In **Tipo provider** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f0799-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="f0799-200">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-200">b.</span></span> <span data-ttu-id="f0799-201">Nella casella di testo **Provider Name** digitare un nome di provider, ad esempio *WAAD*.</span><span class="sxs-lookup"><span data-stu-id="f0799-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="f0799-202">c.</span><span class="sxs-lookup"><span data-stu-id="f0799-202">c.</span></span> <span data-ttu-id="f0799-203">Per caricare il file di metadati scaricato, fare clic su **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="f0799-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="f0799-204">d.</span><span class="sxs-lookup"><span data-stu-id="f0799-204">d.</span></span> <span data-ttu-id="f0799-205">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="f0799-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="f0799-206">Nella pagina della finestra di dialogo **Verify Provider Information** (Verifica informazioni provider) fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f0799-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Configura accesso Single Sign-On][15]

14. <span data-ttu-id="f0799-208">Fare clic su **Ruoli** e quindi fare clic su **Crea nuovo ruolo**.</span><span class="sxs-lookup"><span data-stu-id="f0799-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Configura accesso Single Sign-On][16]

15. <span data-ttu-id="f0799-210">Nella finestra di dialogo **Set Role Name** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Configura accesso Single Sign-On][17] 

    <span data-ttu-id="f0799-212">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-212">a.</span></span> <span data-ttu-id="f0799-213">Nella casella d testo **Role Name** digitare un nome, ad esempio *TestUser*.</span><span class="sxs-lookup"><span data-stu-id="f0799-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="f0799-214">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-214">b.</span></span> <span data-ttu-id="f0799-215">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="f0799-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="f0799-216">Nella finestra di dialogo **Select Role Type** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Configura accesso Single Sign-On][18] 

    <span data-ttu-id="f0799-218">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-218">a.</span></span> <span data-ttu-id="f0799-219">Selezionare **Role For Identity Provider Access**.</span><span class="sxs-lookup"><span data-stu-id="f0799-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="f0799-220">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-220">b.</span></span> <span data-ttu-id="f0799-221">Nella sezione **Grant Web Single Sign-On (WebSSO) access to SAML providers** (Concedi accesso Web Single Sign-On (WebSSO) a provider SAML) fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="f0799-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="f0799-222">Nella finestra di dialogo **Establish Trust** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Configura accesso Single Sign-On][19] 

    <span data-ttu-id="f0799-224">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-224">a.</span></span> <span data-ttu-id="f0799-225">Come provider SAML selezionare quello creato in precedenza, ad esempio *WAAD*</span><span class="sxs-lookup"><span data-stu-id="f0799-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="f0799-226">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-226">b.</span></span> <span data-ttu-id="f0799-227">Fare clic su **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="f0799-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="f0799-228">Nella finestra di dialogo **Verify Role Trust** (Verifica attendibilità ruolo) fare clic su **Passaggio successivo**.</span><span class="sxs-lookup"><span data-stu-id="f0799-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Configura accesso Single Sign-On][32]

19. <span data-ttu-id="f0799-230">Nella finestra di dialogo **Attach Policy** (Allega criteri) fare clic su **Passaggio successivo**.</span><span class="sxs-lookup"><span data-stu-id="f0799-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Configura accesso Single Sign-On][33]

20. <span data-ttu-id="f0799-232">Nella finestra di dialogo **Review** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On][34]
 
    <span data-ttu-id="f0799-234">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-234">a.</span></span> <span data-ttu-id="f0799-235">Fare clic su **Crea ruolo**.</span><span class="sxs-lookup"><span data-stu-id="f0799-235">Click **Create Role**.</span></span>

    <span data-ttu-id="f0799-236">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-236">b.</span></span> <span data-ttu-id="f0799-237">Creare tutti i ruoli necessari in base alle esigenze ed eseguirne il mapping per il Provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f0799-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="f0799-238">Configurare ora il provisioning dell'utente per recuperare tutti i ruoli da AWS</span><span class="sxs-lookup"><span data-stu-id="f0799-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="f0799-239">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-239">a.</span></span> <span data-ttu-id="f0799-240">Nella Console AWS eseguire l'accesso con il proprio account radice</span><span class="sxs-lookup"><span data-stu-id="f0799-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="f0799-241">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-241">b.</span></span> <span data-ttu-id="f0799-242">Nell'angolo superiore destro fare clic sul nome e quindi fare clic sull'opzione **Le mie credenziali di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="f0799-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="f0799-243">Verrà aperta una schermata come messaggio di avviso.</span><span class="sxs-lookup"><span data-stu-id="f0799-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="f0799-244">Fare clic sul pulsante **Credenziali di sicurezza** per passare alla schermata.</span><span class="sxs-lookup"><span data-stu-id="f0799-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Configura accesso Single Sign-On][36]

       ![Configura accesso Single Sign-On][37]

    <span data-ttu-id="f0799-247">c.</span><span class="sxs-lookup"><span data-stu-id="f0799-247">c.</span></span> <span data-ttu-id="f0799-248">Nella sezione Access Keys (Chiavi di accesso) fare clic sul pulsante **Create New Access Key** (Crea nuova chiave di accesso).</span><span class="sxs-lookup"><span data-stu-id="f0799-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="f0799-249">Verrà generata l'ID della chiave di accesso e un valore di token.</span><span class="sxs-lookup"><span data-stu-id="f0799-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Configura accesso Single Sign-On][38]

    <span data-ttu-id="f0799-251">d.</span><span class="sxs-lookup"><span data-stu-id="f0799-251">d.</span></span> <span data-ttu-id="f0799-252">Copiare entrambi questi valori e scaricarli, in modo da non perderli.</span><span class="sxs-lookup"><span data-stu-id="f0799-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="f0799-253">e.</span><span class="sxs-lookup"><span data-stu-id="f0799-253">e.</span></span> <span data-ttu-id="f0799-254">Nella pagina di integrazione dell'applicazione Amazon Web Services (AWS) del Portale di Azure fare clic su **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="f0799-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Configura accesso Single Sign-On][35]

    <span data-ttu-id="f0799-256">f.</span><span class="sxs-lookup"><span data-stu-id="f0799-256">f.</span></span> <span data-ttu-id="f0799-257">Impostare la Modalità di provisioning su **Automatico**</span><span class="sxs-lookup"><span data-stu-id="f0799-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Configura accesso Single Sign-On][39]

    <span data-ttu-id="f0799-259">g.</span><span class="sxs-lookup"><span data-stu-id="f0799-259">g.</span></span> <span data-ttu-id="f0799-260">Ora in **clientsecret** e in **segreto token** incollare i valori corrispondenti, che sono stati copiati dalla Console AWS.</span><span class="sxs-lookup"><span data-stu-id="f0799-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="f0799-261">h.</span><span class="sxs-lookup"><span data-stu-id="f0799-261">h.</span></span> <span data-ttu-id="f0799-262">È possibile fare clic sul pulsante **Test connessione** per testare la connettività.</span><span class="sxs-lookup"><span data-stu-id="f0799-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="f0799-263">Quando questa viene eseguita correttamente è possibile avviare il connettore di provisioning.</span><span class="sxs-lookup"><span data-stu-id="f0799-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Configura accesso Single Sign-On][40]

    <span data-ttu-id="f0799-265">i.</span><span class="sxs-lookup"><span data-stu-id="f0799-265">i.</span></span> <span data-ttu-id="f0799-266">Ora abilitare lo stato di Provisioning su **Attiva**.</span><span class="sxs-lookup"><span data-stu-id="f0799-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="f0799-267">Ciò consente di avviare il recupero dei ruoli dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f0799-267">This starts fetching the roles from the application.</span></span>

       ![Configura accesso Single Sign-On][41]

    > [!NOTE]
    > <span data-ttu-id="f0799-269">Il servizio di provisioning di Azure AD viene eseguito ogni volta dopo un certo lasso di tempo per sincronizzare i ruoli da AWS.</span><span class="sxs-lookup"><span data-stu-id="f0799-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="f0799-270">Vengono visualizzati tutti i ruoli di AWS associati al Provider di identità in Azure AD ed è possibile usarli durante l'assegnazione dell'applicazione a utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="f0799-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0799-271">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0799-272">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0799-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f0799-274">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f0799-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0799-275">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="f0799-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0799-277">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="f0799-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0799-279">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="f0799-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0799-281">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0799-283">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-283">a.</span></span> <span data-ttu-id="f0799-284">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0799-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0799-285">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-285">b.</span></span> <span data-ttu-id="f0799-286">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0799-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0799-287">c.</span><span class="sxs-lookup"><span data-stu-id="f0799-287">c.</span></span> <span data-ttu-id="f0799-288">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="f0799-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0799-289">d.</span><span class="sxs-lookup"><span data-stu-id="f0799-289">d.</span></span> <span data-ttu-id="f0799-290">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f0799-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="f0799-291">Creazione di un utente test in Amazon Web Service</span><span class="sxs-lookup"><span data-stu-id="f0799-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="f0799-292">Per permettere agli utenti di Azure AD di accedere ad Amazon Web Services (AWS), è necessario che eseguano il provisioning in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="f0799-293">Nel caso di Amazon Web Services (AWS), il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f0799-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="f0799-294">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f0799-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f0799-295">Accedere al sito aziendale di **Amazon Web Service (AWS)** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f0799-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="f0799-296">Fare clic sull'icona **Console Home** .</span><span class="sxs-lookup"><span data-stu-id="f0799-296">Click the **Console Home** icon.</span></span> 
   
    ![Configura accesso Single Sign-On][11]

3. <span data-ttu-id="f0799-298">Fare clic su Identity and Access Management.</span><span class="sxs-lookup"><span data-stu-id="f0799-298">Click Identity and Access Management.</span></span> 
   
    ![Configura accesso Single Sign-On][28]

4. <span data-ttu-id="f0799-300">In Dashboard fare clic su **Utenti** e quindi fare clic su **Crea nuovi utenti**.</span><span class="sxs-lookup"><span data-stu-id="f0799-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Configura accesso Single Sign-On][29]

5. <span data-ttu-id="f0799-302">Nella finestra di dialogo Create User seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f0799-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Configura accesso Single Sign-On][30]   
    
    <span data-ttu-id="f0799-304">a.</span><span class="sxs-lookup"><span data-stu-id="f0799-304">a.</span></span> <span data-ttu-id="f0799-305">Nelle caselle di testo **Inserire Nomi Utenti** digitare il nome utente (userprincipalname) di Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0799-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="f0799-306">b.</span><span class="sxs-lookup"><span data-stu-id="f0799-306">b.</span></span> <span data-ttu-id="f0799-307">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f0799-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0799-308">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0799-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0799-309">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Assegna utente][200] 

<span data-ttu-id="f0799-311">**Per assegnare Britta Simon ad Amazon Web Services (AWS), seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="f0799-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="f0799-312">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f0799-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f0799-314">Nell'elenco delle applicazioni selezionare **Amazon Web Service (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="f0799-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="f0799-316">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="f0799-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f0799-318">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f0799-318">Click **Add** button.</span></span> <span data-ttu-id="f0799-319">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f0799-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f0799-321">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="f0799-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0799-322">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f0799-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0799-323">Nella scheda **Seleziona ruolo** selezionare il ruolo appropriato per l'utente.</span><span class="sxs-lookup"><span data-stu-id="f0799-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="f0799-324">Tutti i ruoli vengono visualizzati con il nome del ruolo e il nome del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f0799-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="f0799-325">In questo modo è possibile identificare facilmente i ruoli da AWS.</span><span class="sxs-lookup"><span data-stu-id="f0799-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="f0799-326">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f0799-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0799-327">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f0799-327">Testing single sign-on</span></span>

<span data-ttu-id="f0799-328">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f0799-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0799-329">Quando si fa clic sul riquadro Amazon Web Service (AWS) nel riquadro di accesso, si dovrebbe accedere automaticamente all'applicazione Amazon Web Service (AWS).</span><span class="sxs-lookup"><span data-stu-id="f0799-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0799-330">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f0799-330">Additional resources</span></span>

* [<span data-ttu-id="f0799-331">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0799-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0799-332">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0799-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
