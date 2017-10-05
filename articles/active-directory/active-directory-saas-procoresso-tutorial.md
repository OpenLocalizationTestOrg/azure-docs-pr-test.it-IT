---
title: 'Esercitazione: Integrazione di Azure Active Directory con Procore SSO | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Procore SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="62918-103">Esercitazione: Integrazione di Azure Active Directory con Procore SSO</span><span class="sxs-lookup"><span data-stu-id="62918-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="62918-104">Questa esercitazione descrive come integrare Procore SSO con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62918-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62918-105">L'integrazione di Procore SSO con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="62918-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62918-106">È possibile controllare in Azure AD chi può accedere a Procore SSO</span><span class="sxs-lookup"><span data-stu-id="62918-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="62918-107">È possibile abilitare gli utenti per l'accesso Single Sign-On automatico a Procore SSO con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62918-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="62918-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="62918-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62918-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="62918-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="62918-110">Prerequisites</span></span>

<span data-ttu-id="62918-111">Per configurare l'integrazione di Azure AD con Procore SSO, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="62918-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="62918-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62918-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62918-113">Sottoscrizione di Procore SSO abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="62918-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62918-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="62918-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62918-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62918-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62918-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="62918-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="62918-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62918-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62918-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="62918-118">Scenario description</span></span>
<span data-ttu-id="62918-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="62918-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62918-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="62918-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62918-121">Aggiunta di Procore SSO dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="62918-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="62918-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="62918-123">Aggiungere Procore SSO dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="62918-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="62918-124">Per configurare l'integrazione di Procore SSO in Azure AD, è necessario aggiungere Procore SSO dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="62918-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62918-125">**Per aggiungere Procore SSO dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="62918-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62918-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="62918-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62918-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="62918-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62918-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="62918-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="62918-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="62918-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="62918-133">Nella casella di ricerca digitare **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="62918-133">In the search box, type **Procore SSO**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="62918-135">Nel pannello dei risultati selezionare **Procore SSO** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="62918-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62918-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62918-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Procore SSO con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="62918-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62918-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Procore SSO che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62918-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="62918-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="62918-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="62918-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="62918-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="62918-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Procore SSO, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="62918-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62918-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="62918-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62918-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62918-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62918-145">**[Creazione di un utente test di Procore SSO](#creating-a-procore-sso-test-user)** : per avere una controparte di Britta Simon in Procore SSO collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62918-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="62918-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62918-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62918-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="62918-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62918-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62918-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="62918-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="62918-150">**Per configurare Single Sign-On di Azure AD con Procore SSO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="62918-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="62918-151">Nella pagina di integrazione dell'applicazione **Procore SSO** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="62918-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="62918-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="62918-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="62918-155">Nella sezione **URL e dominio Procore SSO** l'utente deve eseguire alcuna operazione perché l'applicazione è già preintegrata in Azure.</span><span class="sxs-lookup"><span data-stu-id="62918-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="62918-157">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="62918-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="62918-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="62918-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62918-161">Nella sezione **Configurazione di Procore SSO** fare clic su **Configura Procore SSO** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="62918-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="62918-162">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="62918-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="62918-164">Per configurare l'accesso Single Sign-On sul lato **Procore SSO**, accedere al sito aziendale di Procore come amministratore.</span><span class="sxs-lookup"><span data-stu-id="62918-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="62918-165">Nell'elenco della casella degli strumenti scegliere **Admin** per aprire la pagina delle impostazioni SSO.</span><span class="sxs-lookup"><span data-stu-id="62918-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="62918-167">Incollare i valori nelle caselle come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="62918-167">Paste the values in the boxes as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="62918-169">a.</span><span class="sxs-lookup"><span data-stu-id="62918-169">a.</span></span> <span data-ttu-id="62918-170">Incollare l'ID entità SAML copiato dal portale di Azure nella casella **Single Sign On Issuer URL** (URL autorità di certificazione Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="62918-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="62918-171">b.</span><span class="sxs-lookup"><span data-stu-id="62918-171">b.</span></span> <span data-ttu-id="62918-172">Incollare l'URL del servizio Single Sign-On SAML copiato dal portale di Azure nella casella **SAML Sign On Target URL** (URL di destinazione accesso SAML).</span><span class="sxs-lookup"><span data-stu-id="62918-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="62918-173">c.</span><span class="sxs-lookup"><span data-stu-id="62918-173">c.</span></span> <span data-ttu-id="62918-174">Aprire il file **XML dei metadati** scaricato in precedenza dal portale di Azure e copiare il certificato nel tag denominato **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="62918-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="62918-175">Incollare il valore copiato nel **Single Sign On x509 Certificate** (Certificato x509 Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="62918-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="62918-176">Fare clic su **Save Changes** (Salva modifiche).</span><span class="sxs-lookup"><span data-stu-id="62918-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="62918-177">Dopo queste impostazioni, è necessario inviare il **nome di dominio**, ad esempio **contoso.com**, con cui si effettua l'accesso a Procore al [team di supporto Procore](https://support.procore.com/), che attiverà l'accesso Single Sign-On federato per quel dominio.</span><span class="sxs-lookup"><span data-stu-id="62918-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62918-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="62918-179">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="62918-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="62918-181">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="62918-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62918-182">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="62918-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62918-184">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="62918-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62918-186">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="62918-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62918-188">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="62918-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62918-190">a.</span><span class="sxs-lookup"><span data-stu-id="62918-190">a.</span></span> <span data-ttu-id="62918-191">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62918-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62918-192">b.</span><span class="sxs-lookup"><span data-stu-id="62918-192">b.</span></span> <span data-ttu-id="62918-193">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62918-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62918-194">c.</span><span class="sxs-lookup"><span data-stu-id="62918-194">c.</span></span> <span data-ttu-id="62918-195">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="62918-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62918-196">d.</span><span class="sxs-lookup"><span data-stu-id="62918-196">d.</span></span> <span data-ttu-id="62918-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="62918-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="62918-198">Creare un utente test di Procore SSO</span><span class="sxs-lookup"><span data-stu-id="62918-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="62918-199">Attenersi alla procedura seguente per creare un utente test di Procore sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="62918-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="62918-200">Accedere al sito aziendale di Procore come amministratore.</span><span class="sxs-lookup"><span data-stu-id="62918-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="62918-201">Nell'elenco a discesa della casella degli strumenti fare clic su **Directory** per aprire la pagina della directory aziendale.</span><span class="sxs-lookup"><span data-stu-id="62918-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="62918-203">Fare clic su **Add a Person** (Aggiungi una persona) per aprire il modulo e immettere le opzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="62918-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="62918-205">a.</span><span class="sxs-lookup"><span data-stu-id="62918-205">a.</span></span> <span data-ttu-id="62918-206">Digitare il nome di Britta Simon nella casella di testo **First Name** (Nome), ad esempio **Britta**.</span><span class="sxs-lookup"><span data-stu-id="62918-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="62918-207">b.</span><span class="sxs-lookup"><span data-stu-id="62918-207">b.</span></span> <span data-ttu-id="62918-208">Digitare il cognome di Britta Simon nella casella di testo **Last Name** (Cognome), ad esempio **Simon**.</span><span class="sxs-lookup"><span data-stu-id="62918-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="62918-209">c.</span><span class="sxs-lookup"><span data-stu-id="62918-209">c.</span></span> <span data-ttu-id="62918-210">Nella casella di testo **Email Address** (Indirizzo di posta elettronica) digitare l'indirizzo di posta elettronica dell'utente, ad esempio **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="62918-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="62918-211">d.</span><span class="sxs-lookup"><span data-stu-id="62918-211">d.</span></span> <span data-ttu-id="62918-212">Selezionare **Permission Template** (Modello di autorizzazione) per **Apply Permission Template Later** (Applica modello di autorizzazione più tardi).</span><span class="sxs-lookup"><span data-stu-id="62918-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="62918-213">e.</span><span class="sxs-lookup"><span data-stu-id="62918-213">e.</span></span> <span data-ttu-id="62918-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="62918-214">Click **Create**.</span></span>

4. <span data-ttu-id="62918-215">Verificare e aggiornare i dettagli del contatto appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="62918-215">Check and update the details for the newly added contact.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="62918-217">Se è richiesto un invito via posta elettronica, fare clic su **Save and Send Invitation** (Salva e invia invito) oppure scegliere **Save** (Salva) per salvare direttamente e completare la registrazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="62918-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62918-219">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="62918-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62918-220">In questa sezione viene concesso a Britta Simon l'accesso a Procore SSO per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="62918-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Assegna utente][200] 

<span data-ttu-id="62918-222">**Per assegnare Britta Simon a Procore SSO, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="62918-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="62918-223">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="62918-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="62918-225">Nell'elenco di applicazioni selezionare **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="62918-225">In the applications list, select **Procore SSO**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="62918-227">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="62918-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="62918-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="62918-229">Click **Add** button.</span></span> <span data-ttu-id="62918-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="62918-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="62918-232">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="62918-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62918-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="62918-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62918-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="62918-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62918-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="62918-235">Testing single sign-on</span></span>

<span data-ttu-id="62918-236">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="62918-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62918-237">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="62918-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="62918-238">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="62918-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="62918-239">Quando si fa clic sul riquadro Procore SSO nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="62918-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62918-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="62918-240">Additional resources</span></span>

* [<span data-ttu-id="62918-241">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62918-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62918-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62918-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

