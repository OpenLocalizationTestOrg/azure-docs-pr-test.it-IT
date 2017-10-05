---
title: 'Esercitazione: Integrazione di Azure Active Directory con Teamphoria| Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="c917e-103">Esercitazione: Integrazione di Azure Active Directory con Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c917e-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="c917e-104">Questa esercitazione illustra come integrare Teamphoria con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c917e-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c917e-105">L'integrazione di Teamphoria con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c917e-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c917e-106">È possibile controllare in Azure AD chi può accedere a Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c917e-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="c917e-107">È possibile abilitare gli utenti per l'accesso automatico a Teamphoria (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c917e-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="c917e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="c917e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c917e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="c917e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c917e-110">Prerequisites</span></span>

<span data-ttu-id="c917e-111">Per configurare l'integrazione di Azure AD con Teamphoria, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c917e-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="c917e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c917e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c917e-113">Sottoscrizione di Teamphoria abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c917e-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c917e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c917e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c917e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c917e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c917e-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c917e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c917e-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c917e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c917e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c917e-118">Scenario description</span></span>
<span data-ttu-id="c917e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c917e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c917e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c917e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c917e-121">Aggiunta di Teamphoria dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c917e-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="c917e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="c917e-123">Aggiungere Teamphoria dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c917e-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="c917e-124">Per configurare l'integrazione di Teamphoria in Azure AD, è necessario aggiungere Teamphoria dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c917e-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c917e-125">**Per aggiungere Teamphoria dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c917e-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c917e-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c917e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c917e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c917e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c917e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c917e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c917e-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c917e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c917e-133">Digitare **Teamphoria** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c917e-133">In the search box, type **Teamphoria**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="c917e-135">Nel pannello dei risultati selezionare **Teamphoria** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c917e-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c917e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c917e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Teamphoria usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c917e-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c917e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Teamphoria che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c917e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="c917e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c917e-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="c917e-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** (Nome utente) in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c917e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="c917e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Teamphoria, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c917e-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c917e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c917e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c917e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c917e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c917e-145">**[Creazione di un utente test di Teamphoria](#creating-a-teamphoria-test-user)** : per avere una controparte di Britta Simon in Teamphoria collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c917e-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c917e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c917e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c917e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c917e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c917e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c917e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c917e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="c917e-150">**Per configurare l'accesso Single Sign-On di Azure AD con Teamphoria, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c917e-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="c917e-151">Nella pagina di integrazione dell'applicazione **Teamphoria** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c917e-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c917e-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c917e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="c917e-155">Nella sezione **URL e dominio Teamphoria** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c917e-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="c917e-157">a.</span><span class="sxs-lookup"><span data-stu-id="c917e-157">a.</span></span> <span data-ttu-id="c917e-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="c917e-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="c917e-159">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="c917e-159">Please note that these are not the real values.</span></span> <span data-ttu-id="c917e-160">È necessario aggiornare questi valori con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="c917e-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="c917e-161">Contattare il [team di supporto clienti di Teamphoria](https://www.teamphoria.com/) per richiedere l'URL di accesso.</span><span class="sxs-lookup"><span data-stu-id="c917e-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="c917e-162">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c917e-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="c917e-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c917e-164">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c917e-166">Nella sezione **Configurazione di Teamphoria** fare clic su **Configura Teamphoria** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="c917e-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c917e-167">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="c917e-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="c917e-169">Per configurare l'accesso Single Sign-On sul lato **Teamphoria**, accedere all'applicazione Teamphoria come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c917e-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="c917e-170">Passare all'opzione **ADMIN SETTINGS** (Impostazioni di amministrazione) nella barra degli strumenti di sinistra e scegliere **SINGLE SIGN-ON** sotto la scheda di configurazione per aprire la finestra di configurazione SSO.</span><span class="sxs-lookup"><span data-stu-id="c917e-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="c917e-172">Fare clic sull'opzione **ADD NEW IDENTITY PROVIDER** (Aggiungi nuovo provider di identità) nell'angolo superiore destro per aprire il modulo e aggiungere le impostazioni per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c917e-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="c917e-174">Immettere i dettagli nei campi come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="c917e-174">Enter the details in the fields as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="c917e-176">a.</span><span class="sxs-lookup"><span data-stu-id="c917e-176">a.</span></span> <span data-ttu-id="c917e-177">**DISPLAY NAME** (Nome visualizzato): immettere il nome del plug-in visualizzato nella pagina di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="c917e-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="c917e-178">b.</span><span class="sxs-lookup"><span data-stu-id="c917e-178">b.</span></span> <span data-ttu-id="c917e-179">**BUTTON NAME** (Nome pulsante): il nome della scheda che verrà visualizzata nella pagina di accesso per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c917e-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="c917e-180">c.</span><span class="sxs-lookup"><span data-stu-id="c917e-180">c.</span></span> <span data-ttu-id="c917e-181">**CERTIFICATE** (Certificato): aprire il certificato scaricato in precedenza dal portale di Azure nel blocco note, copiare il contenuto dello stesso e incollarlo qui nella casella.</span><span class="sxs-lookup"><span data-stu-id="c917e-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="c917e-182">d.</span><span class="sxs-lookup"><span data-stu-id="c917e-182">d.</span></span> <span data-ttu-id="c917e-183">**ENTRY POINT** (Punto di ingresso): incollare l'**URL del servizio Single Sign-On SAML** copiato in precedenza dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c917e-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="c917e-184">e.</span><span class="sxs-lookup"><span data-stu-id="c917e-184">e.</span></span> <span data-ttu-id="c917e-185">Posizionare il selettore dell'opzione su **ON** e fare clic su **SAVE** (Salva).</span><span class="sxs-lookup"><span data-stu-id="c917e-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c917e-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c917e-187">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c917e-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c917e-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c917e-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c917e-190">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c917e-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c917e-192">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c917e-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c917e-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c917e-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c917e-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c917e-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c917e-198">a.</span><span class="sxs-lookup"><span data-stu-id="c917e-198">a.</span></span> <span data-ttu-id="c917e-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c917e-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c917e-200">b.</span><span class="sxs-lookup"><span data-stu-id="c917e-200">b.</span></span> <span data-ttu-id="c917e-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c917e-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c917e-202">c.</span><span class="sxs-lookup"><span data-stu-id="c917e-202">c.</span></span> <span data-ttu-id="c917e-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c917e-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c917e-204">d.</span><span class="sxs-lookup"><span data-stu-id="c917e-204">d.</span></span> <span data-ttu-id="c917e-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c917e-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="c917e-206">Creare un utente test di Teamphoria</span><span class="sxs-lookup"><span data-stu-id="c917e-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="c917e-207">Per consentire agli utenti di Azure AD di accedere a Teamphoria, è necessario eseguirne il provisioning in Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="c917e-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="c917e-208">Nel caso di Teamphoria, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c917e-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="c917e-209">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c917e-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="c917e-210">Accedere al sito aziendale di Teamphoria come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c917e-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="c917e-211">Fare clic sulle impostazioni **ADMIN** nella barra degli strumenti di sinistra e scegliere **USERS** (Utenti) nella scheda **MANAGE** (Gestisci) per aprire la pagina di amministrazione per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c917e-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="c917e-213">Fare clic sull'opzione **MANUAL INVITE** (Invito manuale).</span><span class="sxs-lookup"><span data-stu-id="c917e-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="c917e-215">In questa pagina effettuare l'operazione seguente.</span><span class="sxs-lookup"><span data-stu-id="c917e-215">On this page, perform following action.</span></span> 
    
    ![Invita persone](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="c917e-217">a.</span><span class="sxs-lookup"><span data-stu-id="c917e-217">a.</span></span> <span data-ttu-id="c917e-218">Nella casella di testo **EMAIL ADDRESS** (Indirizzo email) immettere l'**indirizzo email** di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c917e-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c917e-219">b.</span><span class="sxs-lookup"><span data-stu-id="c917e-219">b.</span></span> <span data-ttu-id="c917e-220">Nella casella di testo **FIRST NAME** (Nome) digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c917e-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="c917e-221">c.</span><span class="sxs-lookup"><span data-stu-id="c917e-221">c.</span></span> <span data-ttu-id="c917e-222">Nella casella di testo **LAST NAME** (Cognome) digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c917e-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="c917e-223">d.</span><span class="sxs-lookup"><span data-stu-id="c917e-223">d.</span></span> <span data-ttu-id="c917e-224">Fare clic su **INVITE 1 USER** (Invita 1 utente).</span><span class="sxs-lookup"><span data-stu-id="c917e-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="c917e-225">L'utente deve accettare l'invito per essere creato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="c917e-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c917e-226">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c917e-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c917e-227">In questa sezione viene concesso a Britta Simon l'accesso a Teamphoria per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="c917e-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c917e-229">**Per assegnare Britta Simon a Teamphoria, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c917e-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="c917e-230">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c917e-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c917e-232">Nell'elenco delle applicazioni selezionare **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="c917e-232">In the applications list, select **Teamphoria**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="c917e-234">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c917e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c917e-236">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c917e-236">Click **Add** button.</span></span> <span data-ttu-id="c917e-237">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c917e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c917e-239">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c917e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c917e-240">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c917e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c917e-241">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c917e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c917e-242">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c917e-242">Testing single sign-on</span></span>

<span data-ttu-id="c917e-243">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c917e-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c917e-244">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c917e-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c917e-245">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c917e-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c917e-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c917e-246">Additional resources</span></span>

* [<span data-ttu-id="c917e-247">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c917e-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c917e-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c917e-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

