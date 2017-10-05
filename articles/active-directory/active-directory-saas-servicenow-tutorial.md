---
title: 'Esercitazione: Integrazione di Azure Active Directory con ServiceNow | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e ServiceNow e ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="2a496-103">Esercitazione: Integrazione di Azure Active Directory con ServiceNow</span><span class="sxs-lookup"><span data-stu-id="2a496-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="2a496-104">Questa esercitazione descrive come integrare ServiceNow e ServiceNow Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a496-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a496-105">L'integrazione di ServiceNow e ServiceNow Express con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="2a496-106">È possibile controllare in Azure AD chi può accedere a ServiceNow e ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="2a496-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="2a496-107">È possibile abilitare gli utenti per l'accesso automatico a ServiceNow e ServiceNow Express (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a496-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="2a496-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="2a496-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="2a496-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a496-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a496-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a496-110">Prerequisites</span></span>
<span data-ttu-id="2a496-111">Per configurare l'integrazione di Azure AD con ServiceNow e ServiceNow Express, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="2a496-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a496-112">An Azure AD subscription</span></span>
* <span data-ttu-id="2a496-113">Per ServiceNow, un'istanza o un tenant di ServiceNow, versione Calgary o successiva</span><span class="sxs-lookup"><span data-stu-id="2a496-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="2a496-114">Per ServiceNow Express, un'istanza di ServiceNow Express, versione Helsinki o successiva</span><span class="sxs-lookup"><span data-stu-id="2a496-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="2a496-115">Nel tenant di ServiceNow deve essere abilitato il [plug-in Multiple Provider Single Sign On](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0).</span><span class="sxs-lookup"><span data-stu-id="2a496-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="2a496-116">Questa operazione può essere eseguita [inviando una richiesta di servizio](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="2a496-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="2a496-117">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2a496-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="2a496-118">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2a496-119">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2a496-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2a496-120">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a496-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a496-121">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2a496-121">Scenario description</span></span>
<span data-ttu-id="2a496-122">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2a496-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a496-123">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a496-124">Aggiunta di ServiceNow dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2a496-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="2a496-125">Configurazione e test dell'accesso Single Sign-On di Azure AD per ServiceNow o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="2a496-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="2a496-126">Aggiunta di ServiceNow dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="2a496-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="2a496-127">Per configurare l'integrazione di ServiceNow o ServiceNow Express in Azure AD, è necessario aggiungere ServiceNow dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2a496-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="2a496-128">**Per aggiungere ServiceNow dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2a496-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a496-129">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2a496-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="2a496-131">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="2a496-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2a496-132">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="2a496-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="2a496-134">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="2a496-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="2a496-136">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="2a496-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="2a496-138">Nella casella di ricerca digitare **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="2a496-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="2a496-140">Nel riquadro dei risultati selezionare **ServiceNow** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a496-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a496-142">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a496-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a496-143">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ServiceNow o ServiceNow Express in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2a496-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a496-144">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di ServiceNow e che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a496-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="2a496-145">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="2a496-146">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="2a496-147">Per configurare e testare l'accesso Single Sign-On di Azure AD con ServiceNow, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a496-148">**[Configurazione dell'accesso Single Sign-On per ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2a496-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a496-149">**[Configurazione dell'accesso Single Sign-On per ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2a496-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="2a496-150">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a496-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2a496-151">**[Creazione di un utente test per ServiceNow](#creating-a-servicenow-test-user)**: per avere una controparte di Britta Simon in ServiceNow collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a496-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="2a496-152">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a496-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="2a496-153">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="2a496-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="2a496-154">Se si vuole configurare ServiceNow, ignorare il passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="2a496-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="2a496-155">Se si vuole configurare ServiceNow Express, ignorare il passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="2a496-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="2a496-156">Configurazione dell'accesso Single Sign-On per ServiceNow</span><span class="sxs-lookup"><span data-stu-id="2a496-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="2a496-157">Nella pagina di integrazione dell'applicazione **ServiceNow** del portale di Azure AD classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2a496-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="2a496-158">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="2a496-159">Nella pagina **Stabilire come si desidera che gli utenti accedano a ServiceNow** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="2a496-160">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="2a496-161">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="2a496-162">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="2a496-163">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-163">a.</span></span> <span data-ttu-id="2a496-164">Nella casella di testo **URL di accesso ServiceNow** digitare l'URL usato dagli utenti per accedere all'applicazione ServiceNow, seguendo il modello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="2a496-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="2a496-165">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-165">b.</span></span> <span data-ttu-id="2a496-166">Nella casella di testo **Identificatore** digitare l'URL usato dagli utenti per accedere all'applicazione ServiceNow, seguendo il modello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="2a496-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="2a496-167">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-167">c.</span></span> <span data-ttu-id="2a496-168">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="2a496-168">Click **Next**</span></span>

4. <span data-ttu-id="2a496-169">Per fare in modo che Azure AD configuri automaticamente ServiceNow per l'autenticazione basata su SAML, immettere il nome dell'istanza ServiceNow, il nome utente amministratore e la password di amministratore nel modulo **Configura automaticamente l'accesso Single Sign-On** e fare clic su *Configura*.</span><span class="sxs-lookup"><span data-stu-id="2a496-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="2a496-170">Affinché la procedura funzioni, il nome utente con diritti amministrativi fornito deve avere il ruolo **security_admin** assegnato in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="2a496-171">In caso contrario, per configurare manualmente ServiceNow per usare Azure AD come provider di identità SAML, fare clic su **Configura manualmente questa applicazione per l'accesso Single Sign-On**, quindi fare clic su **Avanti** e completare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2a496-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="2a496-172">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="2a496-173">Nella pagina **Configura accesso Single Sign-On in ServiceNow** fare clic su **Download certificato** per scaricare il file del certificato e salvarlo nel computer.</span><span class="sxs-lookup"><span data-stu-id="2a496-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="2a496-174">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="2a496-175">Accedere all'applicazione ServiceNow come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2a496-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="2a496-176">Attivare il plug-in *Integration - Multiple Provider Single Sign-On Installer* seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="2a496-177">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-177">a.</span></span> <span data-ttu-id="2a496-178">Nel riquadro di spostamento a sinistra, passare alla sezione **definizione sistema** e quindi fare clic su **Plugins** (Plug-in).</span><span class="sxs-lookup"><span data-stu-id="2a496-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="2a496-179">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Attivare il plug-in")</span><span class="sxs-lookup"><span data-stu-id="2a496-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="2a496-180">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-180">b.</span></span> <span data-ttu-id="2a496-181">Cercare *Integration - Multiple Provider Single Sign-On Installer*.</span><span class="sxs-lookup"><span data-stu-id="2a496-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="2a496-182">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Attivare il plug-in")</span><span class="sxs-lookup"><span data-stu-id="2a496-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="2a496-183">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-183">c.</span></span> <span data-ttu-id="2a496-184">Selezionare il plug-in.</span><span class="sxs-lookup"><span data-stu-id="2a496-184">Select the plugin.</span></span> <span data-ttu-id="2a496-185">Fare clic e selezionare **Activate/Upgrade** (Attiva/Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="2a496-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="2a496-186">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-186">d.</span></span> <span data-ttu-id="2a496-187">Fare clic sul pulsante **Activate** (Attiva).</span><span class="sxs-lookup"><span data-stu-id="2a496-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="2a496-188">Nel riquadro di spostamento a sinistra fare clic su **Properties**.</span><span class="sxs-lookup"><span data-stu-id="2a496-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="2a496-189">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="2a496-190">Nella finestra di dialogo **Multiple Provider SSO Properties** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2a496-191">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="2a496-192">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-192">a.</span></span> <span data-ttu-id="2a496-193">Per **Enable multiple provider SSO** selezionare **Yes**.</span><span class="sxs-lookup"><span data-stu-id="2a496-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="2a496-194">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-194">b.</span></span> <span data-ttu-id="2a496-195">Per **Enable debug logging got the multiple provider SSO integration** selezionare **Yes**.</span><span class="sxs-lookup"><span data-stu-id="2a496-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="2a496-196">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-196">c.</span></span> <span data-ttu-id="2a496-197">Nella casella di testo **The field on the user table that...** digitare **user_name**.</span><span class="sxs-lookup"><span data-stu-id="2a496-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="2a496-198">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-198">d.</span></span> <span data-ttu-id="2a496-199">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="2a496-199">Click **Save**.</span></span>

10. <span data-ttu-id="2a496-200">Nel riquadro di spostamento a sinistra fare clic su **x509 Certificates**.</span><span class="sxs-lookup"><span data-stu-id="2a496-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="2a496-201">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="2a496-202">Nella finestra di dialogo **X.509 Certificates** fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="2a496-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="2a496-203">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="2a496-204">Nella finestra di dialogo **X.509 Certificates** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="2a496-205">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="2a496-206">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-206">a.</span></span> <span data-ttu-id="2a496-207">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="2a496-207">Click **New**.</span></span>
    
     <span data-ttu-id="2a496-208">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-208">b.</span></span> <span data-ttu-id="2a496-209">Nella casella di testo **Name** digitare un nome per la configurazione, ad esempio **TestSAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="2a496-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="2a496-210">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-210">c.</span></span> <span data-ttu-id="2a496-211">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="2a496-211">Select **Active**.</span></span>
    
     <span data-ttu-id="2a496-212">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-212">d.</span></span> <span data-ttu-id="2a496-213">Per **Format** selezionare **PEM**.</span><span class="sxs-lookup"><span data-stu-id="2a496-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="2a496-214">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-214">e.</span></span> <span data-ttu-id="2a496-215">Per **Type** selezionare **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="2a496-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="2a496-216">f.</span><span class="sxs-lookup"><span data-stu-id="2a496-216">f.</span></span> <span data-ttu-id="2a496-217">Aprire il certificato con codifica Base64 in Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **PEM Certificate**.</span><span class="sxs-lookup"><span data-stu-id="2a496-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="2a496-218">g.</span><span class="sxs-lookup"><span data-stu-id="2a496-218">g.</span></span> <span data-ttu-id="2a496-219">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="2a496-219">Click **Update**.</span></span>

13. <span data-ttu-id="2a496-220">Nel riquadro di spostamento a sinistra fare clic su **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="2a496-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="2a496-221">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="2a496-222">Nella finestra di dialogo **Identity Providers** fare clic su **New**:</span><span class="sxs-lookup"><span data-stu-id="2a496-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="2a496-223">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="2a496-224">Nella finestra di dialogo **Identity Providers** fare clic su **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="2a496-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="2a496-225">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="2a496-226">Nella finestra di dialogo SAML2 Update1 Properties seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="2a496-227">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="2a496-228">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-228">a.</span></span> <span data-ttu-id="2a496-229">Nella casella di testo **Nome** digitare un nome per la configurazione (ad esempio **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="2a496-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="2a496-230">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-230">b.</span></span> <span data-ttu-id="2a496-231">Nella casella di testo **User Field** (Campo utente) digitare **email** o **user_name**, a seconda di quale campo viene usato per identificare in modo univoco gli utenti nella distribuzione ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="2a496-232">Per configurare Azure AD per generare l'ID utente di Azure AD, ovvero il nome dell'entità utente, o l'indirizzo di posta elettronica come identificatore univoco nel token SAML, passare alla sezione **ServiceNow > Attributi > Single Sign-On** del portale di Azure classico ed eseguire il mapping del campo scelto all'attributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="2a496-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="2a496-233">Il valore archiviato per l'attributo selezionato in Azure AD (ad esempio il nome dell'entità utente) deve corrispondere al valore archiviato in ServiceNow per il campo immesso (ad esempio user_name)</span><span class="sxs-lookup"><span data-stu-id="2a496-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="2a496-234">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-234">c.</span></span> <span data-ttu-id="2a496-235">Nel portale di Azure AD classico copiare il valore in **ID provider di identità** e incollarlo nella casella di testo **Identity Provider URL** (ID provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="2a496-236">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-236">d.</span></span> <span data-ttu-id="2a496-237">Nel portale di Azure AD classico copiare il valore in **URL richiesta di autenticazione** e incollarlo nella casella di testo **Identity Provider's AuthnRequest** (Richiesta di autenticazione provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="2a496-238">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-238">e.</span></span> <span data-ttu-id="2a496-239">Nel portale di Azure AD classico copiare il valore in **URL servizio Single Sign-Out** e incollarlo nella casella di testo **Identity Provider's SingleLogoutRequest** (Richiesta Single Sign-Out del provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="2a496-240">f.</span><span class="sxs-lookup"><span data-stu-id="2a496-240">f.</span></span> <span data-ttu-id="2a496-241">Nella casella di testo **ServiceNow Homepage** digitare l'URL della home page dell'istanza di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a496-242">L'URL della home page dell'istanza di ServiceNow è una concatenazione dell'**URL del tenant di ServiceNow** e **/navpage.do**, ad esempio `https://fabrikam.service-now.com/navpage.do`.</span><span class="sxs-lookup"><span data-stu-id="2a496-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="2a496-243">g.</span><span class="sxs-lookup"><span data-stu-id="2a496-243">g.</span></span> <span data-ttu-id="2a496-244">Nella casella di testo **Entity ID / Issuer** digitare l'URL del tenant ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="2a496-245">h.</span><span class="sxs-lookup"><span data-stu-id="2a496-245">h.</span></span> <span data-ttu-id="2a496-246">Nella casella di testo **Audience URL** digitare l'URL del tenant ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="2a496-247">i.</span><span class="sxs-lookup"><span data-stu-id="2a496-247">i.</span></span> <span data-ttu-id="2a496-248">Nella casella di testo **Protocol Binding for the IDP's SingleLogoutRequest** digitare **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="2a496-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="2a496-249">j.</span><span class="sxs-lookup"><span data-stu-id="2a496-249">j.</span></span> <span data-ttu-id="2a496-250">Nella casella di testo NameID Policy digitare **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="2a496-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="2a496-251">k.</span><span class="sxs-lookup"><span data-stu-id="2a496-251">k.</span></span> <span data-ttu-id="2a496-252">Fare clic su **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="2a496-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="2a496-253">l.</span><span class="sxs-lookup"><span data-stu-id="2a496-253">l.</span></span> <span data-ttu-id="2a496-254">In **AuthnContextClassRef Method** (Metodo AuthnContextClassRef) digitare `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="2a496-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="2a496-255">Questa operazione è necessaria soltanto per le organizzazioni basate solo su cloud.</span><span class="sxs-lookup"><span data-stu-id="2a496-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="2a496-256">Se si usa AD FS o MFA in locale per l'autenticazione, non è necessario configurare questo valore.</span><span class="sxs-lookup"><span data-stu-id="2a496-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="2a496-257">m.</span><span class="sxs-lookup"><span data-stu-id="2a496-257">m.</span></span> <span data-ttu-id="2a496-258">Nella casella di testo **Clock Skew** digitare **60**.</span><span class="sxs-lookup"><span data-stu-id="2a496-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="2a496-259">n.</span><span class="sxs-lookup"><span data-stu-id="2a496-259">n.</span></span> <span data-ttu-id="2a496-260">Per **Single Sign On Script** selezionare **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="2a496-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="2a496-261">o.</span><span class="sxs-lookup"><span data-stu-id="2a496-261">o.</span></span> <span data-ttu-id="2a496-262">Per **x509 Certificate**selezionare il certificato creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2a496-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="2a496-263">p.</span><span class="sxs-lookup"><span data-stu-id="2a496-263">p.</span></span> <span data-ttu-id="2a496-264">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="2a496-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="2a496-265">Nel portale di Azure AD classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="2a496-266">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="2a496-267">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="2a496-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="2a496-268">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="2a496-269">Configurazione dell'accesso Single Sign-On per ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="2a496-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="2a496-270">Nella pagina di integrazione dell'applicazione **ServiceNow** del portale di Azure AD classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2a496-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="2a496-271">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="2a496-272">Nella pagina **Stabilire come si desidera che gli utenti accedano a ServiceNow** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="2a496-273">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="2a496-274">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="2a496-275">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="2a496-276">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-276">a.</span></span> <span data-ttu-id="2a496-277">Nella casella di testo **URL di accesso ServiceNow** digitare l'URL usato dagli utenti per accedere all'applicazione ServiceNow, seguendo il modello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="2a496-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="2a496-278">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-278">b.</span></span> <span data-ttu-id="2a496-279">Nella casella di testo **URL autorità di certificazione** digitare l'URL usato dagli utenti per accedere all'applicazione ServiceNow, seguendo il modello `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="2a496-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="2a496-280">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-280">c.</span></span> <span data-ttu-id="2a496-281">Fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="2a496-281">Click **Next**</span></span>

4. <span data-ttu-id="2a496-282">Fare clic su **Configura manualmente questa applicazione per l'accesso Single Sign-On**, quindi fare clic su **Avanti** e seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="2a496-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="2a496-283">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="2a496-284">Nella pagina **Configura accesso Single Sign-On in ServiceNow** fare clic su **Download certificato** per scaricare il file del certificato e salvarlo nel computer e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="2a496-285">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="2a496-286">Accedere all'applicazione ServiceNow Express come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2a496-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="2a496-287">Nel riquadro di spostamento a sinistra fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="2a496-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="2a496-288">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="2a496-289">Nella finestra di dialogo **Single Sign-On** fare clic sull'icona di configurazione nell'angolo superiore destro e impostare le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="2a496-290">![Configurare l'URL dell'app](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="2a496-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="2a496-291">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-291">a.</span></span> <span data-ttu-id="2a496-292">Spostare **Enable multiple provider SSO** (Abilita SSO per più provider) verso destra.</span><span class="sxs-lookup"><span data-stu-id="2a496-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="2a496-293">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-293">b.</span></span> <span data-ttu-id="2a496-294">Spostare **Enable debug logging for the multiple provider SSO integration** (Abilita la registrazione debug per l'integrazione SSO per più provider) verso destra.</span><span class="sxs-lookup"><span data-stu-id="2a496-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="2a496-295">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-295">c.</span></span> <span data-ttu-id="2a496-296">Nella casella di testo **The field on the user table that...** digitare **user_name**.</span><span class="sxs-lookup"><span data-stu-id="2a496-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="2a496-297">Nella finestra di dialogo **Single Sign-On** fare clic su **Add New Certificate** (Aggiungi nuovo certificato).</span><span class="sxs-lookup"><span data-stu-id="2a496-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="2a496-298">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="2a496-299">Nella finestra di dialogo **X.509 Certificates** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="2a496-300">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="2a496-301">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-301">a.</span></span> <span data-ttu-id="2a496-302">Nella casella di testo **Name** digitare un nome per la configurazione, ad esempio **TestSAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="2a496-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="2a496-303">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-303">b.</span></span> <span data-ttu-id="2a496-304">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="2a496-304">Select **Active**.</span></span>
    
    <span data-ttu-id="2a496-305">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-305">c.</span></span> <span data-ttu-id="2a496-306">Per **Format** selezionare **PEM**.</span><span class="sxs-lookup"><span data-stu-id="2a496-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="2a496-307">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-307">d.</span></span> <span data-ttu-id="2a496-308">Per **Type** selezionare **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="2a496-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="2a496-309">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-309">e.</span></span> <span data-ttu-id="2a496-310">Creare un file con codifica Base64 dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="2a496-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2a496-311">Per informazioni dettagliate, vedere il video che illustra [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="2a496-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="2a496-312">f.</span><span class="sxs-lookup"><span data-stu-id="2a496-312">f.</span></span> <span data-ttu-id="2a496-313">Aprire il certificato con codifica Base64 in Blocco note, copiarne il contenuto negli Appunti e quindi incollarlo nella casella di testo **PEM Certificate**.</span><span class="sxs-lookup"><span data-stu-id="2a496-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="2a496-314">g.</span><span class="sxs-lookup"><span data-stu-id="2a496-314">g.</span></span> <span data-ttu-id="2a496-315">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="2a496-315">Click **Update**.</span></span>
11. <span data-ttu-id="2a496-316">Nella finestra di dialogo **Single Sign-On** fare clic su **Add New IdP** (Aggiungi nuovo IdP).</span><span class="sxs-lookup"><span data-stu-id="2a496-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="2a496-317">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="2a496-318">Nella finestra di dialogo **Add New Identity Provider** (Aggiungi nuovo provider di identità) in **Configure Identity Provider** (Configura provider di identità) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="2a496-319">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="2a496-320">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-320">a.</span></span> <span data-ttu-id="2a496-321">Nella casella di testo **Name** (Nome) digitare un nome per la configurazione, ad esempio **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2a496-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="2a496-322">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-322">b.</span></span> <span data-ttu-id="2a496-323">Nel portale di Azure AD classico copiare il valore in **ID provider di identità** e incollarlo nella casella di testo **Identity Provider URL** (ID provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="2a496-324">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-324">c.</span></span> <span data-ttu-id="2a496-325">Nel portale di Azure AD classico copiare il valore in **URL richiesta di autenticazione** e incollarlo nella casella di testo **Identity Provider's AuthnRequest** (Richiesta di autenticazione provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="2a496-326">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-326">d.</span></span> <span data-ttu-id="2a496-327">Nel portale di Azure AD classico copiare il valore in **URL servizio Single Sign-Out** e incollarlo nella casella di testo **Identity Provider's SingleLogoutRequest** (Richiesta Single Sign-Out del provider di identità).</span><span class="sxs-lookup"><span data-stu-id="2a496-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="2a496-328">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-328">e.</span></span> <span data-ttu-id="2a496-329">Per **Identity Provider Certificate** (Certificato del provider di identità) selezionare il certificato creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2a496-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="2a496-330">Fare clic su **Advanced Settings** (Impostazioni avanzate). In **Additional Identity Provider Properties** (Proprietà del provider di identità aggiuntivo) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="2a496-331">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="2a496-332">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-332">a.</span></span> <span data-ttu-id="2a496-333">Nella casella di testo **Protocol Binding for the IDP's SingleLogoutRequest** digitare **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="2a496-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="2a496-334">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-334">b.</span></span> <span data-ttu-id="2a496-335">Nella casella di testo **NameID Policy** (Criteri NameID) digitare **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="2a496-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="2a496-336">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-336">c.</span></span> <span data-ttu-id="2a496-337">Nel **metodo AuthnContextClassRef** digitare **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="2a496-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="2a496-338">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-338">d.</span></span> <span data-ttu-id="2a496-339">Fare clic su **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="2a496-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="2a496-340">In **Additional Service Provider Properties** (Proprietà del provider di identità aggiuntivo) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="2a496-341">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="2a496-342">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-342">a.</span></span> <span data-ttu-id="2a496-343">Nella casella di testo **ServiceNow Homepage** digitare l'URL della home page dell'istanza di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2a496-344">L'URL della home page dell'istanza di ServiceNow è una concatenazione dell'**URL del tenant di ServiceNow** e **/navpage.do**, ad esempio `https://fabrikam.service-now.com/navpage.do`.</span><span class="sxs-lookup"><span data-stu-id="2a496-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="2a496-345">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-345">b.</span></span> <span data-ttu-id="2a496-346">Nella casella di testo **Entity ID / Issuer** digitare l'URL del tenant ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="2a496-347">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-347">c.</span></span> <span data-ttu-id="2a496-348">Nella casella di testo **Audience URI** (URI destinatario) digitare l'URL del tenant ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="2a496-349">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-349">d.</span></span> <span data-ttu-id="2a496-350">Nella casella di testo **Clock Skew** digitare **60**.</span><span class="sxs-lookup"><span data-stu-id="2a496-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="2a496-351">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-351">e.</span></span> <span data-ttu-id="2a496-352">Nella casella di testo **User Field** (Campo utente) digitare **email** o **user_name**, a seconda di quale campo viene usato per identificare in modo univoco gli utenti nella distribuzione ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="2a496-353">Per configurare Azure AD per generare l'ID utente di Azure AD, ovvero il nome dell'entità utente, o l'indirizzo di posta elettronica come identificatore univoco nel token SAML, passare alla sezione **ServiceNow > Attributi > Single Sign-On** del portale di Azure classico ed eseguire il mapping del campo scelto all'attributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="2a496-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="2a496-354">Il valore archiviato per l'attributo selezionato in Azure AD (ad esempio il nome dell'entità utente) deve corrispondere al valore archiviato in ServiceNow per il campo immesso (ad esempio user_name)</span><span class="sxs-lookup"><span data-stu-id="2a496-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="2a496-355">f.</span><span class="sxs-lookup"><span data-stu-id="2a496-355">f.</span></span> <span data-ttu-id="2a496-356">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="2a496-356">Click **Save**.</span></span> 

3. <span data-ttu-id="2a496-357">Nel portale di Azure AD classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="2a496-358">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="2a496-359">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="2a496-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="2a496-360">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2a496-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="2a496-361">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="2a496-361">Configuring user provisioning</span></span>
<span data-ttu-id="2a496-362">Questa sezione descrive come abilitare il provisioning degli account utente di Azure Active Directory in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="2a496-363">Per configurare il provisioning utente, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2a496-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="2a496-364">Nella pagina di integrazione dell'applicazione **ServiceNow** del portale di gestione di Azure classico fare clic su **Configura provisioning utenti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="2a496-365">![Provisioning degli utenti](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="2a496-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="2a496-366">Nella pagina **Enter your ServiceNow credentials to enable automatic user provisioning** (Immettere le credenziali Jive per abilitare il provisioning utenti automatico) specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a496-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="2a496-367">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-367">a.</span></span> <span data-ttu-id="2a496-368">Nella casella di testo **Nome istanza ServiceNow** digitare il nome dell'istanza di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="2a496-369">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-369">b.</span></span> <span data-ttu-id="2a496-370">Nella casella di testo **Nome utente amministratore ServiceNow** digitare il nome dell'account amministratore ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="2a496-371">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-371">c.</span></span> <span data-ttu-id="2a496-372">Nella casella di testo **Password amministratore ServiceNow** digitare la password dell'account.</span><span class="sxs-lookup"><span data-stu-id="2a496-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="2a496-373">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-373">d.</span></span> <span data-ttu-id="2a496-374">Fare clic su **Convalida** per verificare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2a496-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="2a496-375">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-375">e.</span></span> <span data-ttu-id="2a496-376">Fare clic sul pulsante **Avanti** per aprire la pagina **Passaggi successivi**.</span><span class="sxs-lookup"><span data-stu-id="2a496-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="2a496-377">f.</span><span class="sxs-lookup"><span data-stu-id="2a496-377">f.</span></span> <span data-ttu-id="2a496-378">Se si vuole eseguire il provisioning di tutti gli utenti nell'applicazione, selezionare "**Esegui automaticamente il provisioning di tutti gli account utente della directory in questa applicazione**".</span><span class="sxs-lookup"><span data-stu-id="2a496-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="2a496-379">![Passaggi successivi](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Passaggi successivi")</span><span class="sxs-lookup"><span data-stu-id="2a496-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="2a496-380">g.</span><span class="sxs-lookup"><span data-stu-id="2a496-380">g.</span></span> <span data-ttu-id="2a496-381">Nella pagina **Passaggi successivi** fare clic su **Completa** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2a496-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a496-382">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a496-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a496-383">In questa sezione viene creato un utente test chiamato Britta Simon nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="2a496-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="2a496-385">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2a496-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a496-386">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="2a496-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="2a496-388">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="2a496-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="2a496-389">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="2a496-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a496-391">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="2a496-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="2a496-393">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="2a496-395">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-395">a.</span></span> <span data-ttu-id="2a496-396">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="2a496-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="2a496-397">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-397">b.</span></span> <span data-ttu-id="2a496-398">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a496-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="2a496-399">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-399">c.</span></span> <span data-ttu-id="2a496-400">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-400">Click **Next**.</span></span>

6. <span data-ttu-id="2a496-401">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="2a496-403">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-403">a.</span></span> <span data-ttu-id="2a496-404">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2a496-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="2a496-405">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-405">b.</span></span> <span data-ttu-id="2a496-406">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2a496-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="2a496-407">c.</span><span class="sxs-lookup"><span data-stu-id="2a496-407">c.</span></span> <span data-ttu-id="2a496-408">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2a496-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="2a496-409">d.</span><span class="sxs-lookup"><span data-stu-id="2a496-409">d.</span></span> <span data-ttu-id="2a496-410">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="2a496-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="2a496-411">e.</span><span class="sxs-lookup"><span data-stu-id="2a496-411">e.</span></span> <span data-ttu-id="2a496-412">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2a496-412">Click **Next**.</span></span>

7. <span data-ttu-id="2a496-413">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="2a496-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="2a496-415">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2a496-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="2a496-417">a.</span><span class="sxs-lookup"><span data-stu-id="2a496-417">a.</span></span> <span data-ttu-id="2a496-418">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="2a496-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="2a496-419">b.</span><span class="sxs-lookup"><span data-stu-id="2a496-419">b.</span></span> <span data-ttu-id="2a496-420">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2a496-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="2a496-421">Creazione di un utente test di ServiceNow</span><span class="sxs-lookup"><span data-stu-id="2a496-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="2a496-422">In questa sezione viene creato un utente di nome Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="2a496-423">In questa sezione viene creato un utente di nome Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="2a496-424">Se non si sa come aggiungere un utente all'account ServiceNow o ServiceNow Express, contattare il team di supporto di ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a496-425">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a496-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="2a496-426">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2a496-428">**Per assegnare Britta Simon a ServiceNow, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="2a496-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="2a496-429">Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="2a496-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][201] 

2. <span data-ttu-id="2a496-431">Nell'elenco di applicazioni, selezionare **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="2a496-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="2a496-433">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="2a496-433">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][203] 

4. <span data-ttu-id="2a496-435">Nell'elenco Tutti gli utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2a496-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="2a496-436">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="2a496-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="2a496-438">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2a496-438">Testing single sign-on</span></span>
<span data-ttu-id="2a496-439">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a496-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a496-440">Quando si fa clic sul riquadro ServiceNow nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="2a496-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a496-441">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2a496-441">Additional resources</span></span>
* [<span data-ttu-id="2a496-442">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a496-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a496-443">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a496-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
