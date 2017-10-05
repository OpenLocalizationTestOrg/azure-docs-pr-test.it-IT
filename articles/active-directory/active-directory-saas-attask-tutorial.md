---
title: 'Esercitazione: Integrazione di Azure Active Directory con @Task| Documenti Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e @Task.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="48c77-103">Esercitazione: Integrazione di Azure Active Directory con @Task</span><span class="sxs-lookup"><span data-stu-id="48c77-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="48c77-104">Questa esercitazione descrive l'integrazione di @Task con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48c77-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="48c77-105">L'integrazione di @Task con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="48c77-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="48c77-106">È possibile controllare in Azure AD chi può accedere a @Task</span><span class="sxs-lookup"><span data-stu-id="48c77-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="48c77-107">È possibile abilitare gli utenti per l'accesso automatico ad @Task (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="48c77-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="48c77-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="48c77-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48c77-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48c77-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="48c77-110">Prerequisites</span></span>
<span data-ttu-id="48c77-111">Per configurare l'integrazione di Azure AD con @Task, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="48c77-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="48c77-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c77-112">An Azure AD subscription</span></span>
* <span data-ttu-id="48c77-113">Sottoscrizione di @Task abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="48c77-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48c77-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="48c77-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="48c77-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="48c77-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="48c77-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="48c77-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="48c77-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48c77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="48c77-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="48c77-118">Scenario Description</span></span>
<span data-ttu-id="48c77-119">L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="48c77-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="48c77-120">Lo scenario descritto in questa esercitazione è costituito da tre blocchi principali:</span><span class="sxs-lookup"><span data-stu-id="48c77-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="48c77-121">Aggiunta di @Task dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="48c77-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="48c77-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="48c77-123">Aggiunta di @Task dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="48c77-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="48c77-124">Per configurare l'integrazione di @Task in Azure AD è necessario aggiungere @Task dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="48c77-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48c77-125">**Per aggiungere @Task dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="48c77-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48c77-126">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="48c77-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="48c77-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="48c77-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="48c77-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="48c77-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2] 
4. <span data-ttu-id="48c77-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="48c77-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3] 
5. <span data-ttu-id="48c77-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="48c77-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4] 
6. <span data-ttu-id="48c77-135">Nella casella di ricerca digitare **@Task**.</span><span class="sxs-lookup"><span data-stu-id="48c77-135">In the search box, type **@Task**.</span></span>
   
    ![Applicazioni][5] 
7. <span data-ttu-id="48c77-137">Nel riquadro dei risultati selezionare **@Task**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="48c77-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Applicazioni][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48c77-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48c77-140">Questa sezione descrive come configurare e testare l'accesso Single Sign-On di Azure AD con @Task in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48c77-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48c77-141">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di @Task che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c77-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="48c77-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="48c77-143">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore di **Username** in @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="48c77-144">Per configurare e testare Azure AD single sign-on con @Task, è necessario completare i seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="48c77-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48c77-145">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="48c77-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48c77-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48c77-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48c77-147">**[Creazione di un utente @Tasktest ](#creating-a-halogen-software-test-user)** per avere una controparte di Britta Simon in @Taskthat collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c77-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="48c77-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c77-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48c77-149">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="48c77-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48c77-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="48c77-151">Questa sezione descrive come abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure classico e configurare l'accesso Single Sign-On nell'applicazione @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="48c77-152">**Per configurare il AD Azure single sign-on con @Task, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48c77-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="48c77-153">Nella pagina di integrazione dell'applicazione **@Task** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="48c77-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="48c77-155">Nella pagina **Stabilire come si desidera che gli utenti accedano a @Task** selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][7] 
3. <span data-ttu-id="48c77-157">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48c77-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configurare le impostazioni dell'app][8] 
   
     <span data-ttu-id="48c77-159">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-159">a.</span></span> <span data-ttu-id="48c77-160">Nella casella di testo **URL di accesso** digitare l'URL utilizzato dagli utenti per accedere all'applicazione @Task, ad esempio:*https://<Tenant name>.attask-ondemand.com*.</span><span class="sxs-lookup"><span data-stu-id="48c77-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="48c77-161">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-161">b.</span></span> <span data-ttu-id="48c77-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-162">Click **Next**.</span></span>
4. <span data-ttu-id="48c77-163">Nella pagina **Configura accesso Single Sign-On in @Task** fare clic su **Scarica metadati**, salvare il file di metadati in locale nel computer e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Cos'è Azure AD Connect][9] 
5. <span data-ttu-id="48c77-165">Accedere al sito aziendale di @Task come amministratore.</span><span class="sxs-lookup"><span data-stu-id="48c77-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="48c77-166">Andare a **Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="48c77-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="48c77-167">Nella finestra di dialogo **Single Sign-On** seguire questa procedura</span><span class="sxs-lookup"><span data-stu-id="48c77-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Configura accesso Single Sign-On][23]
   
    <span data-ttu-id="48c77-169">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-169">a.</span></span> <span data-ttu-id="48c77-170">Per **Type** selezionare**SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="48c77-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="48c77-171">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-171">b.</span></span> <span data-ttu-id="48c77-172">Selezionare **Service Provider ID**.</span><span class="sxs-lookup"><span data-stu-id="48c77-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="48c77-173">c.</span><span class="sxs-lookup"><span data-stu-id="48c77-173">c.</span></span> <span data-ttu-id="48c77-174">Nel portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **Login Portal UR** (URL portale di accesso).</span><span class="sxs-lookup"><span data-stu-id="48c77-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="48c77-175">d.</span><span class="sxs-lookup"><span data-stu-id="48c77-175">d.</span></span> <span data-ttu-id="48c77-176">Nel portale di Azure classico copiare il valore di **URL servizio Single Sign-Out** e incollarlo nella casella di testo **Sign-Out URL** (URL di disconnessione).</span><span class="sxs-lookup"><span data-stu-id="48c77-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="48c77-177">e.</span><span class="sxs-lookup"><span data-stu-id="48c77-177">e.</span></span> <span data-ttu-id="48c77-178">Nel portale di Azure classico copiare il valore di **Modifica URL password** e incollarlo nella casella di testo **Change Password URL** (Modifica URL password).</span><span class="sxs-lookup"><span data-stu-id="48c77-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="48c77-179">f.</span><span class="sxs-lookup"><span data-stu-id="48c77-179">f.</span></span> <span data-ttu-id="48c77-180">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="48c77-180">Click **Save**.</span></span>
8. <span data-ttu-id="48c77-181">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Cos'è Azure AD Connect][10]
9. <span data-ttu-id="48c77-183">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="48c77-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Cos'è Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48c77-185">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="48c77-186">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="48c77-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Creare un utente di Azure AD][20]

<span data-ttu-id="48c77-188">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48c77-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48c77-189">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="48c77-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="48c77-191">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="48c77-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="48c77-192">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="48c77-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="48c77-194">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="48c77-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="48c77-196">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48c77-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="48c77-198">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-198">a.</span></span> <span data-ttu-id="48c77-199">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="48c77-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="48c77-200">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-200">b.</span></span> <span data-ttu-id="48c77-201">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48c77-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="48c77-202">c.</span><span class="sxs-lookup"><span data-stu-id="48c77-202">c.</span></span> <span data-ttu-id="48c77-203">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-203">Click **Next**.</span></span>
6. <span data-ttu-id="48c77-204">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48c77-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="48c77-206">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-206">a.</span></span> <span data-ttu-id="48c77-207">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="48c77-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="48c77-208">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-208">b.</span></span> <span data-ttu-id="48c77-209">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="48c77-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="48c77-210">c.</span><span class="sxs-lookup"><span data-stu-id="48c77-210">c.</span></span> <span data-ttu-id="48c77-211">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="48c77-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="48c77-212">d.</span><span class="sxs-lookup"><span data-stu-id="48c77-212">d.</span></span> <span data-ttu-id="48c77-213">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="48c77-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="48c77-214">e.</span><span class="sxs-lookup"><span data-stu-id="48c77-214">e.</span></span> <span data-ttu-id="48c77-215">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="48c77-215">Click **Next**.</span></span>

7. <span data-ttu-id="48c77-216">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="48c77-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="48c77-218">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48c77-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="48c77-220">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-220">a.</span></span> <span data-ttu-id="48c77-221">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="48c77-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="48c77-222">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-222">b.</span></span> <span data-ttu-id="48c77-223">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="48c77-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="48c77-224">Creazione di un utente di test di @Task</span><span class="sxs-lookup"><span data-stu-id="48c77-224">Creating an @Task test user</span></span>
<span data-ttu-id="48c77-225">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="48c77-226">**Per creare un utente denominato Britta Simon in @Task, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48c77-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="48c77-227">Accedere al sito aziendale di @Task come amministratore.</span><span class="sxs-lookup"><span data-stu-id="48c77-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="48c77-228">Nel menu in alto fare clic su **People**.</span><span class="sxs-lookup"><span data-stu-id="48c77-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="48c77-229">Fare clic su **New Person**.</span><span class="sxs-lookup"><span data-stu-id="48c77-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="48c77-230">Nella finestra di dialogo New Person seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48c77-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Creare un utente di test di @Task][21] 
   
    <span data-ttu-id="48c77-232">a.</span><span class="sxs-lookup"><span data-stu-id="48c77-232">a.</span></span> <span data-ttu-id="48c77-233">Nella casella di testo **First Name** digitare "Britta".</span><span class="sxs-lookup"><span data-stu-id="48c77-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="48c77-234">b.</span><span class="sxs-lookup"><span data-stu-id="48c77-234">b.</span></span> <span data-ttu-id="48c77-235">Nella casella di testo **Last Name** digitare "Simon".</span><span class="sxs-lookup"><span data-stu-id="48c77-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="48c77-236">c.</span><span class="sxs-lookup"><span data-stu-id="48c77-236">c.</span></span> <span data-ttu-id="48c77-237">Nella casella di testo **Email Address** digitare l'indirizzo di posta elettronica di Britta Simon in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48c77-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="48c77-238">d.</span><span class="sxs-lookup"><span data-stu-id="48c77-238">d.</span></span> <span data-ttu-id="48c77-239">Fare clic su **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="48c77-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48c77-240">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c77-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="48c77-241">L'obiettivo di questa sezione consiste nell'abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Assegna utente][200] 

<span data-ttu-id="48c77-243">**Per assegnare Britta Simon a @Task, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="48c77-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="48c77-244">Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="48c77-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][201] 
2. <span data-ttu-id="48c77-246">Nell'elenco delle applicazioni selezionare **@Task**.</span><span class="sxs-lookup"><span data-stu-id="48c77-246">In the applications list, select **@Task**.</span></span>
   
    ![Assegna utente][202] 
3. <span data-ttu-id="48c77-248">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="48c77-248">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][203] 
4. <span data-ttu-id="48c77-250">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="48c77-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="48c77-251">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="48c77-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="48c77-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="48c77-253">Testing Single Sign-On</span></span>
<span data-ttu-id="48c77-254">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="48c77-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="48c77-255">Quando si fa clic sul riquadro @Task nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione @Task.</span><span class="sxs-lookup"><span data-stu-id="48c77-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48c77-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="48c77-256">Additional Resources</span></span>
* [<span data-ttu-id="48c77-257">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c77-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48c77-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c77-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






