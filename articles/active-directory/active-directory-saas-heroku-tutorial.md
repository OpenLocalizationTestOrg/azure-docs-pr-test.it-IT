---
title: 'Esercitazione: Integrazione di Azure Active Directory con Heroku | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Heroku.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="1bfc0-103">Esercitazione: Integrazione di Azure Active Directory con Heroku</span><span class="sxs-lookup"><span data-stu-id="1bfc0-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="1bfc0-104">Questa esercitazione descrive come integrare Heroku con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bfc0-105">L'integrazione di Heroku con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1bfc0-106">È possibile controllare in Azure AD chi può accedere a Heroku</span><span class="sxs-lookup"><span data-stu-id="1bfc0-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="1bfc0-107">È possibile abilitare gli utenti per l'accesso automatico a Heroku (Single Sign-On) con l'account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bfc0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1bfc0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bfc0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1bfc0-110">Prerequisites</span></span>

<span data-ttu-id="1bfc0-111">Per configurare l'integrazione di Azure AD con Heroku, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="1bfc0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bfc0-113">Sottoscrizione di Heroku abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1bfc0-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bfc0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bfc0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bfc0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bfc0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bfc0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1bfc0-118">Scenario description</span></span>
<span data-ttu-id="1bfc0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bfc0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bfc0-121">Aggiunta di Heroku dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1bfc0-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="1bfc0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="1bfc0-123">Aggiunta di Heroku dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="1bfc0-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="1bfc0-124">Per configurare l'integrazione di Heroku in Azure AD, è necessario aggiungere Heroku dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1bfc0-125">**Per aggiungere Heroku dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1bfc0-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1bfc0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1bfc0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1bfc0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1bfc0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1bfc0-133">Nella casella di ricerca digitare **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-133">In the search box, type **Heroku**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="1bfc0-135">Nel pannello dei risultati selezionare **Heroku** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1bfc0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1bfc0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Heroku con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1bfc0-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1bfc0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Heroku che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="1bfc0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Heroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="1bfc0-141">Per stabilire la relazione di collegamento, in Heroku assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1bfc0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Heroku, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1bfc0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1bfc0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bfc0-145">**[Creazione di un utente test di Heroku](#creating-a-heroku-test-user)** : per avere una controparte di Britta Simon in Heroku collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bfc0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bfc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1bfc0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1bfc0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Heroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="1bfc0-150">**Per configurare l'accesso Single Sign-On di Azure AD con Heroku, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1bfc0-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="1bfc0-151">Nella pagina di integrazione dell'applicazione **Heroku** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1bfc0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="1bfc0-155">Nella sezione **URL e dominio Heroku** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="1bfc0-157">a.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-157">a.</span></span> <span data-ttu-id="1bfc0-158">Nella casella di testo **URL di accesso** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="1bfc0-159">b.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-159">b.</span></span> <span data-ttu-id="1bfc0-160">Nella casella di testo **Identificatore** digitare un URL usando il criterio seguente:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="1bfc0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1bfc0-161">These values are not real.</span></span> <span data-ttu-id="1bfc0-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1bfc0-163">Questi valori vengono comunicati dal team di Heroku, come descritto nelle sezioni successive di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="1bfc0-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="1bfc0-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1bfc0-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1bfc0-168">Per abilitare l'accesso Single Sign-On in Heroku, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="1bfc0-169">a.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-169">a.</span></span> <span data-ttu-id="1bfc0-170">Accedere all'account Heroku come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="1bfc0-171">b.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-171">b.</span></span> <span data-ttu-id="1bfc0-172">Fare clic sulla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="1bfc0-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="1bfc0-173">c.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-173">c.</span></span> <span data-ttu-id="1bfc0-174">Nella pagina **Single Sign On** fare clic su **Upload Metadata** (Carica metadati).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="1bfc0-175">d.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-175">d.</span></span> <span data-ttu-id="1bfc0-176">Caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="1bfc0-177">e.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-177">e.</span></span> <span data-ttu-id="1bfc0-178">Al termine dell'installazione agli amministratori viene visualizzata una finestra di dialogo di conferma e l'URL di accesso Single Sign-On per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="1bfc0-179">f.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-179">f.</span></span> <span data-ttu-id="1bfc0-180">Copiare i valori di **URL di accesso Heroku** e **ID entità Heroku**, tornare alla sezione **URL e dominio Heroku** nel portale di Azure e incollare questi valori rispettivamente nelle caselle di testo **URL di accesso Sign-On** e **Identificatore**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="1bfc0-182">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="1bfc0-183">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1bfc0-184">Dopo aver aggiunto l'app dalla sezione **Applicazioni aziendali Active Directory** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1bfc0-185">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1bfc0-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="1bfc0-187">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1bfc0-189">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1bfc0-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1bfc0-190">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bfc0-192">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bfc0-194">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bfc0-196">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1bfc0-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bfc0-198">a.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-198">a.</span></span> <span data-ttu-id="1bfc0-199">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bfc0-200">b.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-200">b.</span></span> <span data-ttu-id="1bfc0-201">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bfc0-202">c.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-202">c.</span></span> <span data-ttu-id="1bfc0-203">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1bfc0-204">d.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-204">d.</span></span> <span data-ttu-id="1bfc0-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="1bfc0-206">Creazione di un utente test di Heroku</span><span class="sxs-lookup"><span data-stu-id="1bfc0-206">Creating a Heroku test user</span></span>

<span data-ttu-id="1bfc0-207">In questa sezione viene creato un utente chiamato Britta Simon in Heroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="1bfc0-208">Heroku supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="1bfc0-209">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-209">There is no action item for you in this section.</span></span> <span data-ttu-id="1bfc0-210">Quando si accede a Heroku se l'utente non esiste ancora, viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="1bfc0-211">Dopo il provisioning dell'account, l'utente finale riceve un messaggio di verifica e deve fare clic sul collegamento di conferma.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="1bfc0-212">Per creare un utente manualmente, è necessario contattare il [team di supporto di client Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="1bfc0-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1bfc0-213">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bfc0-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1bfc0-214">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Heroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1bfc0-216">**Per assegnare Britta Simon a Heroku, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1bfc0-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="1bfc0-217">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1bfc0-219">Nell'elenco di applicazioni selezionare **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-219">In the applications list, select **Heroku**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="1bfc0-221">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1bfc0-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-223">Click **Add** button.</span></span> <span data-ttu-id="1bfc0-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1bfc0-226">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1bfc0-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bfc0-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1bfc0-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1bfc0-229">Testing single sign-on</span></span>

<span data-ttu-id="1bfc0-230">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1bfc0-231">Quando si fa clic sul riquadro Heroku nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione Heroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc0-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bfc0-232">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1bfc0-232">Additional resources</span></span>

* [<span data-ttu-id="1bfc0-233">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bfc0-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bfc0-234">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bfc0-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
