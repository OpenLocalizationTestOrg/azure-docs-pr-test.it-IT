---
title: 'Esercitazione: Integrazione di Azure Active Directory con Showpad | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Showpad.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: c8b39c9215675d8073f896f934339e7cd55334cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="364af-103">Esercitazione: Integrazione di Azure Active Directory con Showpad</span><span class="sxs-lookup"><span data-stu-id="364af-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="364af-104">Questa esercitazione descrive come integrare Showpad con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="364af-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="364af-105">L'integrazione di Showpad con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="364af-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="364af-106">È possibile controllare in Azure AD chi può accedere a Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="364af-107">È possibile abilitare gli utenti per l'accesso automatico a Showpad (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364af-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="364af-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="364af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="364af-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="364af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="364af-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="364af-110">Prerequisites</span></span>

<span data-ttu-id="364af-111">Per configurare l'integrazione di Azure AD con Showpad, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="364af-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="364af-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="364af-113">Sottoscrizione Showpad abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="364af-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="364af-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="364af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="364af-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="364af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="364af-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="364af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="364af-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="364af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="364af-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="364af-118">Scenario description</span></span>
<span data-ttu-id="364af-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="364af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="364af-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="364af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="364af-121">Aggiunta di Showpad dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="364af-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="364af-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="364af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="364af-123">Aggiunta di Showpad dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="364af-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="364af-124">Per configurare l'integrazione di Showpad in Azure AD, è necessario aggiungere Showpad dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="364af-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="364af-125">**Per aggiungere Showpad dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="364af-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="364af-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="364af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="364af-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="364af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="364af-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="364af-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="364af-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="364af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="364af-133">Nella casella di ricerca digitare **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="364af-133">In the search box, type **Showpad**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="364af-135">Nel pannello dei risultati selezionare **Showpad** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="364af-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="364af-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="364af-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="364af-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Showpad in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="364af-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="364af-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Showpad che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="364af-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="364af-141">Per stabilire la relazione di collegamento, in Showpad assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="364af-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="364af-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Showpad, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="364af-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="364af-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="364af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="364af-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="364af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="364af-145">**[Creazione di un utente di test di Showpad](#creating-a-showpad-test-user)**: per avere una controparte di Britta Simon in Showpad collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364af-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="364af-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="364af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="364af-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="364af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="364af-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="364af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="364af-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="364af-150">**Per configurare l'accesso Single Sign-On di Azure AD con Showpad, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="364af-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="364af-151">Nella pagina di integrazione dell'applicazione **Showpad** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="364af-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="364af-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="364af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="364af-155">Nella sezione **URL e dominio Showpad** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="364af-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="364af-157">a.</span><span class="sxs-lookup"><span data-stu-id="364af-157">a.</span></span> <span data-ttu-id="364af-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<comapany-name>.showpad.biz/login`.</span><span class="sxs-lookup"><span data-stu-id="364af-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="364af-159">b.</span><span class="sxs-lookup"><span data-stu-id="364af-159">b.</span></span> <span data-ttu-id="364af-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="364af-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="364af-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="364af-161">These values are not real.</span></span> <span data-ttu-id="364af-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="364af-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="364af-163">Per ottenere questi valori, contattare il [team di supporto di Showpad](https://help.showpad.com).</span><span class="sxs-lookup"><span data-stu-id="364af-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


4. <span data-ttu-id="364af-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="364af-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="364af-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="364af-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="364af-168">Accedere al tenant di Showpad come amministratore.</span><span class="sxs-lookup"><span data-stu-id="364af-168">Sign-on to your Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="364af-169">Scegliere **Settings**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="364af-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="364af-171">Passare a "**Single Sign-On**" e fare clic su "**Enable**".</span><span class="sxs-lookup"><span data-stu-id="364af-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="364af-173">Nella finestra di dialogo **Add a SAML 2.0 Service** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="364af-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="364af-175">a.</span><span class="sxs-lookup"><span data-stu-id="364af-175">a.</span></span> <span data-ttu-id="364af-176">Nella casella di testo **Nome** digitare il nome del provider di identità (ad esempio, il nome della propria società).</span><span class="sxs-lookup"><span data-stu-id="364af-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="364af-177">b.</span><span class="sxs-lookup"><span data-stu-id="364af-177">b.</span></span> <span data-ttu-id="364af-178">In **Metadata Source** (Origine metadati) selezionare **XML**.</span><span class="sxs-lookup"><span data-stu-id="364af-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="364af-179">c.</span><span class="sxs-lookup"><span data-stu-id="364af-179">c.</span></span> <span data-ttu-id="364af-180">Copiare il contenuto del file XML di metadati scaricato dal portale di Azure e quindi incollarlo nella casella di testo **Metadata XML** .</span><span class="sxs-lookup"><span data-stu-id="364af-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="364af-181">d.</span><span class="sxs-lookup"><span data-stu-id="364af-181">d.</span></span> <span data-ttu-id="364af-182">Selezionare **Auto-provision accounts for new users when they log in**.</span><span class="sxs-lookup"><span data-stu-id="364af-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="364af-183">e.</span><span class="sxs-lookup"><span data-stu-id="364af-183">e.</span></span> <span data-ttu-id="364af-184">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="364af-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="364af-185">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="364af-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="364af-186">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="364af-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="364af-187">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="364af-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="364af-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="364af-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="364af-189">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="364af-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="364af-191">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="364af-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="364af-192">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="364af-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="364af-194">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="364af-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="364af-196">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="364af-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="364af-198">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="364af-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="364af-200">a.</span><span class="sxs-lookup"><span data-stu-id="364af-200">a.</span></span> <span data-ttu-id="364af-201">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="364af-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="364af-202">b.</span><span class="sxs-lookup"><span data-stu-id="364af-202">b.</span></span> <span data-ttu-id="364af-203">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="364af-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="364af-204">c.</span><span class="sxs-lookup"><span data-stu-id="364af-204">c.</span></span> <span data-ttu-id="364af-205">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="364af-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="364af-206">d.</span><span class="sxs-lookup"><span data-stu-id="364af-206">d.</span></span> <span data-ttu-id="364af-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="364af-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="364af-208">Creazione di un utente test di Showpad</span><span class="sxs-lookup"><span data-stu-id="364af-208">Creating a Showpad test user</span></span>

<span data-ttu-id="364af-209">Questa sezione descrive come creare un utente chiamato Britta Simon in Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="364af-210">Showpad supporta il provisioning just-in-time.</span><span class="sxs-lookup"><span data-stu-id="364af-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="364af-211">Il provisioning è stato abilitato in **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="364af-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="364af-212">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="364af-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="364af-213">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="364af-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="364af-214">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![Assegna utente][200] 

<span data-ttu-id="364af-216">**Per assegnare Britta Simon a Showpad, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="364af-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="364af-217">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="364af-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="364af-219">Nell'elenco di applicazioni selezionare **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="364af-219">In the applications list, select **Showpad**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="364af-221">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="364af-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="364af-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="364af-223">Click **Add** button.</span></span> <span data-ttu-id="364af-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="364af-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="364af-226">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="364af-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="364af-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="364af-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="364af-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="364af-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="364af-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="364af-229">Testing single sign-on</span></span>

<span data-ttu-id="364af-230">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="364af-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="364af-231">Quando si fa clic sul riquadro Showpad nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Showpad.</span><span class="sxs-lookup"><span data-stu-id="364af-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="364af-232">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="364af-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="364af-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="364af-233">Additional resources</span></span>

* [<span data-ttu-id="364af-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="364af-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="364af-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="364af-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

