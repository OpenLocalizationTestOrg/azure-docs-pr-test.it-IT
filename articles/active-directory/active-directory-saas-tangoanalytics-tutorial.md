---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tango Analytics | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Tango Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 46f6facc3c86630a9252340b2e89634368c0263d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="c0235-103">Esercitazione: Integrazione di Azure Active Directory con Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="c0235-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="c0235-104">Questa esercitazione descrive come integrare Tango Analytics con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0235-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0235-105">L'integrazione di Tango Analytics con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0235-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0235-106">È possibile controllare in Azure AD chi può accedere a Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="c0235-106">You can control in Azure AD who has access to Tango Analytics</span></span>
- <span data-ttu-id="c0235-107">È possibile abilitare gli utenti per l'accesso automatico a Tango Analytics (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0235-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0235-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0235-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0235-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0235-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c0235-110">Prerequisites</span></span>

<span data-ttu-id="c0235-111">Per configurare l'integrazione di Azure AD con Tango Analytics, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0235-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span></span>

- <span data-ttu-id="c0235-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0235-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0235-113">Sottoscrizione di Tango Analytics abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0235-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0235-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c0235-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0235-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0235-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0235-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c0235-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0235-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0235-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0235-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="c0235-118">Scenario description</span></span>
<span data-ttu-id="c0235-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="c0235-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0235-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0235-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0235-121">Aggiunta di Tango Analytics dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c0235-121">Adding Tango Analytics from the gallery</span></span>
2. <span data-ttu-id="c0235-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-the-gallery"></a><span data-ttu-id="c0235-123">Aggiunta di Tango Analytics dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="c0235-123">Adding Tango Analytics from the gallery</span></span>
<span data-ttu-id="c0235-124">Per configurare l'integrazione di Tango Analytics in Azure AD, è necessario aggiungere Tango Analytics dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="c0235-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0235-125">**Per aggiungere Tango Analytics dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0235-125">**To add Tango Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0235-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c0235-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0235-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="c0235-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0235-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0235-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="c0235-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0235-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="c0235-133">Nella casella di ricerca digitare **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c0235-133">In the search box, type **Tango Analytics**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

5. <span data-ttu-id="c0235-135">Nel pannello dei risultati selezionare **Tango Analytics** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0235-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0235-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0235-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tango Analytics usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c0235-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0235-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Tango Analytics che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0235-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="c0235-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span></span>

<span data-ttu-id="c0235-141">Per stabilire la relazione di collegamento, in Tango Analytics assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="c0235-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0235-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Tango Analytics, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0235-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0235-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c0235-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0235-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0235-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0235-145">**[Creazione di un utente di test di Tango Analytics](#creating-a-tango-analytics-test-user)**: per avere una controparte di Britta Simon in Tango Analytics collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0235-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0235-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0235-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0235-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="c0235-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0235-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0235-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="c0235-150">**Per configurare l'accesso Single Sign-On di Azure AD con Tango Analytics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0235-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="c0235-151">Nella pagina di integrazione dell'applicazione **Tango Analytics** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c0235-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="c0235-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c0235-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

3. <span data-ttu-id="c0235-155">Nella sezione **URL e dominio Tango Analytics** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c0235-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="c0235-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0235-157">a.</span></span> <span data-ttu-id="c0235-158">Nella casella di testo **Identificatore** digitare il valore `TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="c0235-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span></span>

    <span data-ttu-id="c0235-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0235-159">b.</span></span> <span data-ttu-id="c0235-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="c0235-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0235-161">Il valore di URL di risposta non è reale.</span><span class="sxs-lookup"><span data-stu-id="c0235-161">The Reply URL value is not real.</span></span> <span data-ttu-id="c0235-162">È necessario aggiornarlo con l'URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="c0235-162">Update this with the actual Reply URL.</span></span> <span data-ttu-id="c0235-163">Per ottenere tale valore, contattare il [team di supporto di Tango Analytics](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="c0235-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span></span>

4. <span data-ttu-id="c0235-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c0235-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

5. <span data-ttu-id="c0235-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="c0235-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0235-168">Per configurare l'accesso Single Sign-On sul lato **Tango Analytics**, è necessario inviare il file **XML dei metadati** scaricato al [team di supporto di Tango Analytics](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="c0235-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="c0235-169">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="c0235-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0235-170">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="c0235-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0235-171">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="c0235-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0235-172">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0235-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0235-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0235-174">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0235-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="c0235-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="c0235-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0235-177">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c0235-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0235-179">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="c0235-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0235-181">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="c0235-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0235-183">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c0235-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0235-185">a.</span><span class="sxs-lookup"><span data-stu-id="c0235-185">a.</span></span> <span data-ttu-id="c0235-186">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0235-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0235-187">b.</span><span class="sxs-lookup"><span data-stu-id="c0235-187">b.</span></span> <span data-ttu-id="c0235-188">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0235-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0235-189">c.</span><span class="sxs-lookup"><span data-stu-id="c0235-189">c.</span></span> <span data-ttu-id="c0235-190">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="c0235-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0235-191">d.</span><span class="sxs-lookup"><span data-stu-id="c0235-191">d.</span></span> <span data-ttu-id="c0235-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0235-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="c0235-193">Creazione di un utente di test di Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="c0235-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="c0235-194">In questa sezione viene creato un utente chiamato Britta Simon in Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="c0235-195">Collaborare con il [team di supporto di Tango Analytics](mailto:support@tangoanalytics.com) per aggiungere gli utenti nella piattaforma Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span></span> <span data-ttu-id="c0235-196">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c0235-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0235-197">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0235-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0235-198">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span></span>

![Assegna utente][200] 

<span data-ttu-id="c0235-200">**Per assegnare Britta Simon a Tango Analytics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c0235-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="c0235-201">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c0235-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="c0235-203">Nell'elenco di applicazioni selezionare **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c0235-203">In the applications list, select **Tango Analytics**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

3. <span data-ttu-id="c0235-205">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c0235-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="c0235-207">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0235-207">Click **Add** button.</span></span> <span data-ttu-id="c0235-208">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0235-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="c0235-210">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="c0235-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0235-211">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="c0235-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0235-212">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="c0235-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0235-213">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c0235-213">Testing single sign-on</span></span>

<span data-ttu-id="c0235-214">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c0235-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0235-215">Quando si fa clic sul riquadro Tango Analytics nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="c0235-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span></span>
<span data-ttu-id="c0235-216">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0235-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0235-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c0235-217">Additional resources</span></span>

* [<span data-ttu-id="c0235-218">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0235-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0235-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0235-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoanalytics-tutorial/tutorial_general_203.png

