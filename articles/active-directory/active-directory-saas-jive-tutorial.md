---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jive | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="26f95-103">Esercitazione: Integrazione di Azure Active Directory con Jive</span><span class="sxs-lookup"><span data-stu-id="26f95-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="26f95-104">Questa esercitazione descrive come integrare Jive con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26f95-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26f95-105">L'integrazione di Jive con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26f95-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26f95-106">È possibile controllare in Azure AD chi può accedere a Jive</span><span class="sxs-lookup"><span data-stu-id="26f95-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="26f95-107">È possibile abilitare gli utenti per l'accesso automatico a Jive (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26f95-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26f95-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26f95-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26f95-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26f95-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="26f95-110">Prerequisites</span></span>

<span data-ttu-id="26f95-111">Per configurare l'integrazione di Azure AD con Jive, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26f95-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="26f95-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26f95-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26f95-113">Sottoscrizione di Jive abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26f95-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26f95-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="26f95-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26f95-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="26f95-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26f95-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="26f95-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26f95-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26f95-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26f95-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="26f95-118">Scenario description</span></span>
<span data-ttu-id="26f95-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="26f95-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26f95-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26f95-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26f95-121">Aggiunta di Jive dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26f95-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="26f95-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="26f95-123">Aggiunta di Jive dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="26f95-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="26f95-124">Per configurare l'integrazione di Jive in Azure AD, è necessario aggiungere Jive dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="26f95-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26f95-125">**Per aggiungere Jive dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26f95-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26f95-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26f95-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26f95-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="26f95-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26f95-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26f95-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="26f95-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="26f95-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="26f95-133">Nella casella di ricerca digitare **Jive**.</span><span class="sxs-lookup"><span data-stu-id="26f95-133">In the search box, type **Jive**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="26f95-135">Nel pannello dei risultati selezionare **Jive** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26f95-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26f95-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26f95-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jive in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26f95-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="26f95-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Jive che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26f95-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="26f95-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="26f95-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **nome utente** in Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="26f95-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Jive, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="26f95-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26f95-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="26f95-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26f95-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26f95-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26f95-145">**[Creazione di un utente di test di Jive](#creating-a-jive-test-user)**: per avere una controparte di Britta Simon in Jive collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26f95-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26f95-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26f95-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26f95-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="26f95-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26f95-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26f95-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="26f95-150">**Per configurare l'accesso Single Sign-On di Azure AD con Jive, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26f95-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="26f95-151">Nella pagina di integrazione dell'applicazione **Jive** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="26f95-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="26f95-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="26f95-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="26f95-155">Nella sezione **URL e dominio Jive** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26f95-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="26f95-157">a.</span><span class="sxs-lookup"><span data-stu-id="26f95-157">a.</span></span> <span data-ttu-id="26f95-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<instance name>.jivecustom.com`.</span><span class="sxs-lookup"><span data-stu-id="26f95-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="26f95-159">b.</span><span class="sxs-lookup"><span data-stu-id="26f95-159">b.</span></span> <span data-ttu-id="26f95-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="26f95-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26f95-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="26f95-161">These values are not the real.</span></span> <span data-ttu-id="26f95-162">è necessario aggiornarli con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="26f95-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="26f95-163">Per ottenere questi valori, contattare il [team di supporto client di Jive](https://www.jivesoftware.com/services-support/).</span><span class="sxs-lookup"><span data-stu-id="26f95-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="26f95-164">Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.</span><span class="sxs-lookup"><span data-stu-id="26f95-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="26f95-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="26f95-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="26f95-168">Per configurare l'accesso single sign-on sul lato **Jive**, accedere al tenant Jive come amministratore.</span><span class="sxs-lookup"><span data-stu-id="26f95-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="26f95-169">Nel menu in alto fare clic su "**Saml**".</span><span class="sxs-lookup"><span data-stu-id="26f95-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="26f95-171">a.</span><span class="sxs-lookup"><span data-stu-id="26f95-171">a.</span></span> <span data-ttu-id="26f95-172">Selezionare **Abilitato** nella scheda **Generale**.</span><span class="sxs-lookup"><span data-stu-id="26f95-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="26f95-173">b.</span><span class="sxs-lookup"><span data-stu-id="26f95-173">b.</span></span> <span data-ttu-id="26f95-174">Fare clic sul pulsante**Save all SAML settings**(Salva tutte le impostazioni SAML).</span><span class="sxs-lookup"><span data-stu-id="26f95-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="26f95-175">Passare alla scheda**IdP Metadata**(Metadati IdP).</span><span class="sxs-lookup"><span data-stu-id="26f95-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="26f95-177">a.</span><span class="sxs-lookup"><span data-stu-id="26f95-177">a.</span></span> <span data-ttu-id="26f95-178">Copiare il contenuto del file XML di metadati scaricato e incollarlo nella casella di testo **Identity Provider (IdP) Metadata** (Metadati del provider di identità - IdP).</span><span class="sxs-lookup"><span data-stu-id="26f95-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="26f95-179">b.</span><span class="sxs-lookup"><span data-stu-id="26f95-179">b.</span></span> <span data-ttu-id="26f95-180">Fare clic sul pulsante**Save all SAML settings**(Salva tutte le impostazioni SAML).</span><span class="sxs-lookup"><span data-stu-id="26f95-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="26f95-181">Passare alla scheda**User Attribute Mapping**(Mapping degli attributi utente).</span><span class="sxs-lookup"><span data-stu-id="26f95-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="26f95-183">a.</span><span class="sxs-lookup"><span data-stu-id="26f95-183">a.</span></span> <span data-ttu-id="26f95-184">Nella casella di testo **Email** copiare e incollare il nome dell'attributo del valore **mail**.</span><span class="sxs-lookup"><span data-stu-id="26f95-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="26f95-185">b.</span><span class="sxs-lookup"><span data-stu-id="26f95-185">b.</span></span> <span data-ttu-id="26f95-186">Nella casella di testo **Nome** copiare e incollare il nome dell'attributo del valore **givenname**.</span><span class="sxs-lookup"><span data-stu-id="26f95-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="26f95-187">c.</span><span class="sxs-lookup"><span data-stu-id="26f95-187">c.</span></span> <span data-ttu-id="26f95-188">Nella casella di testo **Cognome** copiare e incollare il nome dell'attributo del valore **surname**.</span><span class="sxs-lookup"><span data-stu-id="26f95-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="26f95-189">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="26f95-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26f95-190">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="26f95-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26f95-191">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26f95-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26f95-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="26f95-193">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="26f95-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="26f95-195">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="26f95-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26f95-196">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="26f95-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26f95-198">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="26f95-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26f95-200">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="26f95-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26f95-202">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26f95-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26f95-204">a.</span><span class="sxs-lookup"><span data-stu-id="26f95-204">a.</span></span> <span data-ttu-id="26f95-205">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26f95-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26f95-206">b.</span><span class="sxs-lookup"><span data-stu-id="26f95-206">b.</span></span> <span data-ttu-id="26f95-207">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="26f95-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26f95-208">c.</span><span class="sxs-lookup"><span data-stu-id="26f95-208">c.</span></span> <span data-ttu-id="26f95-209">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="26f95-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26f95-210">d.</span><span class="sxs-lookup"><span data-stu-id="26f95-210">d.</span></span> <span data-ttu-id="26f95-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="26f95-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="26f95-212">Creazione di un utente test di Jive</span><span class="sxs-lookup"><span data-stu-id="26f95-212">Creating a Jive test user</span></span>

<span data-ttu-id="26f95-213">Collaborare con il [team di supporto client di Jive](https://www.jivesoftware.com/services-support/) per aggiungere gli utenti alla piattaforma Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26f95-214">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="26f95-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26f95-215">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Assegna utente][200] 

<span data-ttu-id="26f95-217">**Per assegnare Britta Simon a Jive, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="26f95-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="26f95-218">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26f95-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="26f95-220">Nell'elenco delle applicazioni selezionare **Jive**.</span><span class="sxs-lookup"><span data-stu-id="26f95-220">In the applications list, select **Jive**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="26f95-222">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="26f95-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="26f95-224">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="26f95-224">Click **Add** button.</span></span> <span data-ttu-id="26f95-225">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26f95-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="26f95-227">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="26f95-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26f95-228">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26f95-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26f95-229">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="26f95-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26f95-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="26f95-230">Testing single sign-on</span></span>

<span data-ttu-id="26f95-231">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="26f95-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26f95-232">Quando si fa clic sul riquadro Jive nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Jive.</span><span class="sxs-lookup"><span data-stu-id="26f95-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26f95-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="26f95-233">Additional resources</span></span>

* [<span data-ttu-id="26f95-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26f95-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26f95-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26f95-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="26f95-236">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="26f95-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

