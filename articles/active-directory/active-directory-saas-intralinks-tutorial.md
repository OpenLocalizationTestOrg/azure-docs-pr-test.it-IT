---
title: 'Esercitazione: Integrazione di Azure Active Directory con Intralinks | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="a097c-103">Esercitazione: Integrazione di Azure Active Directory con Intralinks</span><span class="sxs-lookup"><span data-stu-id="a097c-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="a097c-104">Questa esercitazione descrive come integrare Intralinks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a097c-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a097c-105">L'integrazione di Intralinks con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a097c-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a097c-106">È possibile controllare in Azure AD chi può accedere a Intralinks</span><span class="sxs-lookup"><span data-stu-id="a097c-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="a097c-107">È possibile abilitare gli utenti per l'accesso automatico a Intralinks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a097c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a097c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a097c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a097c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a097c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a097c-110">Prerequisites</span></span>

<span data-ttu-id="a097c-111">Per configurare l'integrazione di Azure AD con Intralinks, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a097c-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="a097c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a097c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a097c-113">Sottoscrizione Intralinks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a097c-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a097c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a097c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a097c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a097c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a097c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a097c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a097c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a097c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a097c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a097c-118">Scenario description</span></span>
<span data-ttu-id="a097c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a097c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a097c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a097c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a097c-121">Aggiunta di Intralinks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a097c-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="a097c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="a097c-123">Aggiunta di Intralinks dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a097c-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="a097c-124">Per configurare l'integrazione di Intralinks in Azure AD, è necessario aggiungere Intralinks dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a097c-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a097c-125">**Per aggiungere Intralinks dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a097c-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a097c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a097c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a097c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a097c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a097c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a097c-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a097c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a097c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a097c-133">Nella casella di ricerca digitare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a097c-133">In the search box, type **Intralinks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="a097c-135">Nel pannello dei risultati selezionare **Intralinks** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a097c-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a097c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a097c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Intralinks con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a097c-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a097c-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Intralinks che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a097c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="a097c-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="a097c-141">Per stabilire la relazione di collegamento, in Intralinks assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="a097c-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a097c-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Intralinks, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a097c-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a097c-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a097c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a097c-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a097c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a097c-145">**[Creazione di un utente di test di Intralinks](#creating-an-intralinks-test-user)**: per avere una controparte di Britta Simon in Intralinks collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a097c-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a097c-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a097c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a097c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a097c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a097c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a097c-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="a097c-150">**Per configurare l'accesso Single Sign-On di Azure AD con Intralinks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a097c-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="a097c-151">Nella pagina di integrazione dell'applicazione **Intralinks** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a097c-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a097c-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a097c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="a097c-155">Nella sezione **URL e dominio Intralinks** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a097c-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="a097c-157">Nella casella di testo **URL di accesso** digitare l'URL usando il criterio seguente: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="a097c-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a097c-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="a097c-158">This value is not real.</span></span> <span data-ttu-id="a097c-159">aggiornarlo con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="a097c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a097c-160">Per ottenere questo valore, contattare il [team di supporto client di Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="a097c-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="a097c-161">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="a097c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="a097c-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a097c-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a097c-165">Per configurare l'accesso Single Sign-On sul lato **Intralinks**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="a097c-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="a097c-166">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="a097c-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a097c-167">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="a097c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a097c-168">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="a097c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a097c-169">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a097c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a097c-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a097c-171">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a097c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a097c-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a097c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a097c-174">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a097c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a097c-176">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="a097c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a097c-178">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a097c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a097c-180">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a097c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a097c-182">a.</span><span class="sxs-lookup"><span data-stu-id="a097c-182">a.</span></span> <span data-ttu-id="a097c-183">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a097c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a097c-184">b.</span><span class="sxs-lookup"><span data-stu-id="a097c-184">b.</span></span> <span data-ttu-id="a097c-185">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a097c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a097c-186">c.</span><span class="sxs-lookup"><span data-stu-id="a097c-186">c.</span></span> <span data-ttu-id="a097c-187">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="a097c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a097c-188">d.</span><span class="sxs-lookup"><span data-stu-id="a097c-188">d.</span></span> <span data-ttu-id="a097c-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a097c-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="a097c-190">Creazione di un utente test di Intralinks</span><span class="sxs-lookup"><span data-stu-id="a097c-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="a097c-191">In questa sezione viene creato un utente chiamato Britta Simon in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="a097c-192">Collaborare con il [team di supporto di Intralinks](https://www.intralinks.com/contact-1) per aggiungere gli utenti nella piattaforma Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a097c-193">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a097c-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a097c-194">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a097c-196">**Per assegnare Britta Simon a Intralinks, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a097c-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="a097c-197">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a097c-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a097c-199">Nell'elenco di applicazioni selezionare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a097c-199">In the applications list, select **Intralinks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="a097c-201">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="a097c-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a097c-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a097c-203">Click **Add** button.</span></span> <span data-ttu-id="a097c-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a097c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a097c-206">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="a097c-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a097c-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a097c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a097c-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a097c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="a097c-209">Aggiungere un'applicazione Intralinks VIA o Elite</span><span class="sxs-lookup"><span data-stu-id="a097c-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="a097c-210">Intralinks usa la stessa piattaforma di identità SSO per tutte le altre applicazioni Intralinks esclusa applicazione Deal Nexus.</span><span class="sxs-lookup"><span data-stu-id="a097c-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="a097c-211">Se si prevede di usare qualsiasi altra applicazione Intralinks, è necessario configurare prima di tutto l'accesso SSO per un'applicazione di Intralinks primaria usando la procedura descritta sopra.</span><span class="sxs-lookup"><span data-stu-id="a097c-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="a097c-212">Si potrà quindi usare la procedura seguente per aggiungere un'altra applicazione Intralinks nel tenant che può sfruttare l'applicazione primaria per SSO.</span><span class="sxs-lookup"><span data-stu-id="a097c-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="a097c-213">Questa funzionalità è disponibile solo per i clienti degli SKU di Azure AD Premium e non per i clienti di SKU Basic o Gratuito.</span><span class="sxs-lookup"><span data-stu-id="a097c-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="a097c-214">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a097c-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="a097c-216">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a097c-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a097c-217">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a097c-217">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a097c-219">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="a097c-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a097c-221">Nella casella di ricerca digitare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a097c-221">In the search box, type **Intralinks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="a097c-223">In **Intralinks Aggiungi app** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a097c-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Aggiunta di un'applicazione Intralinks VIA o Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="a097c-225">a.</span><span class="sxs-lookup"><span data-stu-id="a097c-225">a.</span></span> <span data-ttu-id="a097c-226">Nella casella di testo **Nome** immettere un nome appropriato per l'applicazione, ad esempio **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="a097c-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="a097c-227">b.</span><span class="sxs-lookup"><span data-stu-id="a097c-227">b.</span></span> <span data-ttu-id="a097c-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a097c-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="a097c-229">Nella pagina di integrazione dell'applicazione **Intralinks** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a097c-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

7. <span data-ttu-id="a097c-231">Nella finestra di dialogo **Single Sign-On** selezionare **Modalità** come **Accesso collegato**.</span><span class="sxs-lookup"><span data-stu-id="a097c-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="a097c-233">Ottenere l'URL SSO avviato dal provider di servizi dal [team Intralinks](https://www.intralinks.com/contact-1) per l'altra applicazione Intralinks e immetterlo in **Configurare l'URL di accesso** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a097c-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="a097c-235">Nella casella di testo URL accesso digitare l'URL utilizzato dagli utenti per accedere all'applicazione Intralinks adottando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="a097c-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="a097c-236">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a097c-236">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="a097c-238">Assegnare l'applicazione a un utente o a gruppi, come illustrato nella sezione **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="a097c-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="a097c-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a097c-239">Testing single sign-on</span></span>

<span data-ttu-id="a097c-240">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a097c-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a097c-241">Quando si fa clic sul riquadro Intralinks nel pannello di accesso, si accede automaticamente all'applicazione Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a097c-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="a097c-242">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a097c-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a097c-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a097c-243">Additional resources</span></span>

* [<span data-ttu-id="a097c-244">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a097c-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a097c-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a097c-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

