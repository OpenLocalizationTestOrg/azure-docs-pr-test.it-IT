---
title: 'Esercitazione: Integrazione di Azure Active Directory con SmarterU | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SmarterU.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="32be7-103">Esercitazione: Integrazione di Azure Active Directory con SmarterU</span><span class="sxs-lookup"><span data-stu-id="32be7-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="32be7-104">Questa esercitazione descrive come integrare SmarterU con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32be7-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32be7-105">L'integrazione di SmarterU con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32be7-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32be7-106">È possibile controllare in Azure AD chi può accedere a SmarterU</span><span class="sxs-lookup"><span data-stu-id="32be7-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="32be7-107">È possibile abilitare gli utenti per l'accesso automatico a SmarterU (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="32be7-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32be7-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32be7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32be7-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32be7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32be7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32be7-110">Prerequisites</span></span>

<span data-ttu-id="32be7-111">Per configurare l'integrazione di Azure AD con SmarterU, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32be7-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="32be7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32be7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32be7-113">Sottoscrizione di SmarterU abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32be7-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32be7-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32be7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32be7-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="32be7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32be7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="32be7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32be7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32be7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32be7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="32be7-118">Scenario description</span></span>
<span data-ttu-id="32be7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="32be7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32be7-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="32be7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32be7-121">Aggiunta di SmarterU dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32be7-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="32be7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32be7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="32be7-123">Aggiunta di SmarterU dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="32be7-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="32be7-124">Per configurare l'integrazione di SmarterU in Azure AD, è necessario aggiungere SmarterU dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="32be7-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32be7-125">**Per aggiungere SmarterU dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32be7-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32be7-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32be7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32be7-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="32be7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32be7-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32be7-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="32be7-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="32be7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="32be7-133">Nella casella di ricerca digitare **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="32be7-133">In the search box, type **SmarterU**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="32be7-135">Nel pannello dei risultati selezionare **SmarterU** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32be7-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32be7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32be7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32be7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SmarterU usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32be7-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32be7-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di SmarterU corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32be7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="32be7-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SmarterU.</span><span class="sxs-lookup"><span data-stu-id="32be7-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="32be7-141">Per stabilire la relazione di collegamento, in SmarterU assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="32be7-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32be7-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con SmarterU, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="32be7-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32be7-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="32be7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32be7-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32be7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32be7-145">**[Creazione di un utente di test di SmarterU](#creating-a-smarteru-test-user)**: per avere una controparte di Britta Simon in SmarterU collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32be7-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32be7-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32be7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32be7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="32be7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32be7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32be7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32be7-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione SmarterU.</span><span class="sxs-lookup"><span data-stu-id="32be7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="32be7-150">**Per configurare l'accesso Single Sign-On di Azure AD con SmarterU, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32be7-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="32be7-151">Nella pagina di integrazione dell'applicazione **SmarterU** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="32be7-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="32be7-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="32be7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="32be7-155">Nella sezione **URL e dominio SmarterU** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32be7-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="32be7-157">Nella casella di testo **Identificatore** digitare l'URL: `https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="32be7-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="32be7-158">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="32be7-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="32be7-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="32be7-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32be7-162">In un'altra finestra del Web browser accedere al sito aziendale di SmarterU come amministratore.</span><span class="sxs-lookup"><span data-stu-id="32be7-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="32be7-163">Nella barra degli strumenti in alto fare clic su **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="32be7-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="32be7-164">![Impostazioni account](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="32be7-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="32be7-165">Nella pagina di configurazione dell’account, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32be7-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="32be7-166">![Autorizzazione esterna](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorizzazione esterna")</span><span class="sxs-lookup"><span data-stu-id="32be7-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="32be7-167">a.</span><span class="sxs-lookup"><span data-stu-id="32be7-167">a.</span></span> <span data-ttu-id="32be7-168">Selezionare **Attiva autorizzazione esterna**.</span><span class="sxs-lookup"><span data-stu-id="32be7-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="32be7-169">b.</span><span class="sxs-lookup"><span data-stu-id="32be7-169">b.</span></span> <span data-ttu-id="32be7-170">Nella sezione **Controllo accesso master** selezionare la scheda **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="32be7-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="32be7-171">c.</span><span class="sxs-lookup"><span data-stu-id="32be7-171">c.</span></span> <span data-ttu-id="32be7-172">Nella sezione **Accesso predefinito utente** selezionare la scheda **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="32be7-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="32be7-173">d.</span><span class="sxs-lookup"><span data-stu-id="32be7-173">d.</span></span> <span data-ttu-id="32be7-174">Selezionare **Attiva Okta**.</span><span class="sxs-lookup"><span data-stu-id="32be7-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="32be7-175">e.</span><span class="sxs-lookup"><span data-stu-id="32be7-175">e.</span></span> <span data-ttu-id="32be7-176">Copiare il contenuto del file dei metadati scaricato e incollarlo nella casella di testo **Metadati Okta** .</span><span class="sxs-lookup"><span data-stu-id="32be7-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="32be7-177">f.</span><span class="sxs-lookup"><span data-stu-id="32be7-177">f.</span></span> <span data-ttu-id="32be7-178">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="32be7-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="32be7-179">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="32be7-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32be7-180">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="32be7-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32be7-181">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32be7-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32be7-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32be7-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="32be7-183">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32be7-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="32be7-185">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="32be7-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32be7-186">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="32be7-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32be7-188">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="32be7-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32be7-190">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="32be7-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32be7-192">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32be7-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32be7-194">a.</span><span class="sxs-lookup"><span data-stu-id="32be7-194">a.</span></span> <span data-ttu-id="32be7-195">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32be7-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32be7-196">b.</span><span class="sxs-lookup"><span data-stu-id="32be7-196">b.</span></span> <span data-ttu-id="32be7-197">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32be7-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32be7-198">c.</span><span class="sxs-lookup"><span data-stu-id="32be7-198">c.</span></span> <span data-ttu-id="32be7-199">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="32be7-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32be7-200">d.</span><span class="sxs-lookup"><span data-stu-id="32be7-200">d.</span></span> <span data-ttu-id="32be7-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="32be7-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="32be7-202">Creazione di un utente di test di SmarterU</span><span class="sxs-lookup"><span data-stu-id="32be7-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="32be7-203">Per consentire agli utenti di Azure AD di accedere a SmarterU, è necessario effettuarne il provisioning in SmarterU.</span><span class="sxs-lookup"><span data-stu-id="32be7-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="32be7-204">Nel caso di SmarterU, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="32be7-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="32be7-205">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32be7-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="32be7-206">Accedere al tenant **SmarterU** .</span><span class="sxs-lookup"><span data-stu-id="32be7-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="32be7-207">Andare a **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="32be7-207">Go to **Users**.</span></span>

3. <span data-ttu-id="32be7-208">Nella sezione degli utenti, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="32be7-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="32be7-209">![Nuovo utente](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="32be7-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="32be7-210">a.</span><span class="sxs-lookup"><span data-stu-id="32be7-210">a.</span></span> <span data-ttu-id="32be7-211">Fare clic su **+Utente**.</span><span class="sxs-lookup"><span data-stu-id="32be7-211">Click **+User**.</span></span>
    
    <span data-ttu-id="32be7-212">b.</span><span class="sxs-lookup"><span data-stu-id="32be7-212">b.</span></span> <span data-ttu-id="32be7-213">Digitare i valori degli attributi correlati dell'account utente Azure AD nelle caselle di testo seguenti: **Posta elettronica principale**, **ID dipendente**, **Password**, **Verifica password**, **Nome**, **Cognome**.</span><span class="sxs-lookup"><span data-stu-id="32be7-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="32be7-214">c.</span><span class="sxs-lookup"><span data-stu-id="32be7-214">c.</span></span> <span data-ttu-id="32be7-215">Fare clic su **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="32be7-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="32be7-216">d.</span><span class="sxs-lookup"><span data-stu-id="32be7-216">d.</span></span> <span data-ttu-id="32be7-217">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="32be7-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="32be7-218">È possibile usare qualsiasi altro strumento di creazione di account utentedi SmarterU o API fornita da SmarterU per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32be7-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32be7-219">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="32be7-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32be7-220">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SmarterU.</span><span class="sxs-lookup"><span data-stu-id="32be7-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![Assegna utente][200] 

<span data-ttu-id="32be7-222">**Per assegnare Britta Simon a SmarterU, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="32be7-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="32be7-223">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="32be7-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="32be7-225">Nell'elenco delle applicazioni selezionare **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="32be7-225">In the applications list, select **SmarterU**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="32be7-227">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="32be7-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="32be7-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="32be7-229">Click **Add** button.</span></span> <span data-ttu-id="32be7-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32be7-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="32be7-232">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="32be7-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32be7-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="32be7-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32be7-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="32be7-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32be7-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="32be7-235">Testing single sign-on</span></span>

<span data-ttu-id="32be7-236">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="32be7-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="32be7-237">Quando si fa clic sul riquadro SmarterU nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SmarterU.</span><span class="sxs-lookup"><span data-stu-id="32be7-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="32be7-238">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32be7-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="32be7-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="32be7-239">Additional resources</span></span>

* [<span data-ttu-id="32be7-240">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32be7-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32be7-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32be7-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

