---
title: 'Esercitazione: integrazione di Azure Active Directory con ASC Contracts | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ASC Contracts.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="dd72b-103">Esercitazione: integrazione di Azure Active Directory con ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="dd72b-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="dd72b-104">Questa esercitazione descrive come integrare ASC Contracts con Azure Active Directory, ovvero Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd72b-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd72b-105">L'integrazione di ASC Contracts con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd72b-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd72b-106">È possibile controllare in Azure AD chi può accedere ad ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="dd72b-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="dd72b-107">È possibile abilitare gli utenti per l'accesso automatico, Single Sign-On, ad ASC Contracts con i propri account di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd72b-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd72b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd72b-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd72b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd72b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd72b-110">Prerequisites</span></span>

<span data-ttu-id="dd72b-111">Per configurare l'integrazione di Azure AD con ASC Contracts, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd72b-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="dd72b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd72b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd72b-113">Sottoscrizione di ASC Contracts abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd72b-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd72b-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dd72b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd72b-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd72b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd72b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dd72b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd72b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd72b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd72b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dd72b-118">Scenario description</span></span>
<span data-ttu-id="dd72b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dd72b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd72b-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd72b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd72b-121">Aggiunta di ASC Contracts dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dd72b-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="dd72b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="dd72b-123">Aggiunta di ASC Contracts dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dd72b-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="dd72b-124">Per configurare l'integrazione di ASC Contracts in Azure AD, è necessario aggiungere ASC Contracts dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dd72b-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd72b-125">**Per aggiungere ASC Contracts dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd72b-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd72b-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dd72b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd72b-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd72b-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dd72b-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd72b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dd72b-133">Nella casella di ricerca digitare **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-133">In the search box, type **ASC Contracts**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="dd72b-135">Nel pannello dei risultati selezionare **ASC Contracts** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd72b-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd72b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd72b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ASC Contracts usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dd72b-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd72b-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di ASC Contracts che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd72b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="dd72b-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="dd72b-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="dd72b-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con ASC Contracts, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd72b-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd72b-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dd72b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd72b-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd72b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd72b-145">**[Creazione di un utente di test di ASC Contracts](#creating-an-asc-contracts-test-user)**: per avere una controparte di Britta Simon in ASC Contracts collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd72b-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd72b-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd72b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd72b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="dd72b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd72b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd72b-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="dd72b-150">**Per configurare l'accesso Single Sign-On di Azure AD con ASC Contracts, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd72b-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="dd72b-151">Nella pagina di integrazione dell'applicazione **ASC Contracts** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dd72b-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dd72b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="dd72b-155">Nella sezione **ASC Contracts Domain and URLs** (URL e dominio ASC Contracts) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd72b-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="dd72b-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd72b-157">a.</span></span> <span data-ttu-id="dd72b-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="dd72b-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="dd72b-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd72b-159">b.</span></span> <span data-ttu-id="dd72b-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="dd72b-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd72b-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dd72b-161">These values are not real.</span></span> <span data-ttu-id="dd72b-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="dd72b-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dd72b-163">Contattare il team di ASC Networks Inc. (ASC) al numero **613.599.6178** per ottenere questi valori.</span><span class="sxs-lookup"><span data-stu-id="dd72b-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="dd72b-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="dd72b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="dd72b-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dd72b-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd72b-168">Per configurare l'accesso Single Sign-On sul lato **ASC Contracts**, chiamare il supporto di ASC Networks Inc. (ASC) al numero **613.599.6178** e dare il file **XML metadati** scaricato.</span><span class="sxs-lookup"><span data-stu-id="dd72b-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="dd72b-169">L'applicazione verrà configurata in modo che la connessione SAML SSO sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="dd72b-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="dd72b-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="dd72b-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd72b-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dd72b-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd72b-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd72b-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd72b-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd72b-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd72b-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dd72b-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dd72b-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd72b-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dd72b-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd72b-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="dd72b-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd72b-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd72b-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dd72b-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd72b-185">a.</span><span class="sxs-lookup"><span data-stu-id="dd72b-185">a.</span></span> <span data-ttu-id="dd72b-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd72b-187">b.</span><span class="sxs-lookup"><span data-stu-id="dd72b-187">b.</span></span> <span data-ttu-id="dd72b-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd72b-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd72b-189">c.</span><span class="sxs-lookup"><span data-stu-id="dd72b-189">c.</span></span> <span data-ttu-id="dd72b-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd72b-191">d.</span><span class="sxs-lookup"><span data-stu-id="dd72b-191">d.</span></span> <span data-ttu-id="dd72b-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="dd72b-193">Creazione di un utente test di ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="dd72b-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="dd72b-194">Rivolgersi al team di supporto di ASC Networks Inc. (ASC) al numero **613.599.6178** per ottenere gli utenti aggiunti alla piattaforma di ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd72b-195">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd72b-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd72b-196">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso ad ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dd72b-198">**Per assegnare Britta Simon a ASC Contracts, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dd72b-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="dd72b-199">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dd72b-201">Nell'elenco di applicazioni, selezionare **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="dd72b-203">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dd72b-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dd72b-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-205">Click **Add** button.</span></span> <span data-ttu-id="dd72b-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dd72b-208">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="dd72b-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd72b-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd72b-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dd72b-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd72b-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dd72b-211">Testing single sign-on</span></span>

<span data-ttu-id="dd72b-212">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dd72b-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd72b-213">Quando si fa clic sul riquadro di ASC Contracts nel riquadro di accesso, si dovrebbe accedere automaticamente all'applicazione ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="dd72b-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="dd72b-214">Per ulteriori informazioni sul pannello di accesso, vedere</span><span class="sxs-lookup"><span data-stu-id="dd72b-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="dd72b-215">[Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586)</span><span class="sxs-lookup"><span data-stu-id="dd72b-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd72b-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dd72b-216">Additional resources</span></span>

* [<span data-ttu-id="dd72b-217">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd72b-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd72b-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd72b-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

