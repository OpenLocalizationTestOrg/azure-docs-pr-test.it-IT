---
title: 'Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e SciQuest Spend Director.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 84b707668dc45e92e6151f422f1c919f638533b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="a4431-103">Esercitazione: Integrazione di Azure Active Directory con SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="a4431-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="a4431-104">Questa esercitazione descrive l’integrazione di SciQuest Spend Director con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4431-104">The objective of this tutorial is to show you how to integrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="a4431-105">L'integrazione di SciQuest Spend Director con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4431-105">Integrating SciQuest Spend Director with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="a4431-106">È possibile controllare in Azure AD chi può accedere a SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-106">You can control in Azure AD who has access to SciQuest Spend Director</span></span> 
* <span data-ttu-id="a4431-107">È possibile abilitare gli utenti per l'accesso automatico a SciQuest Spend Director (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4431-107">You can enable your users to automatically get signed-on to SciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a4431-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="a4431-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="a4431-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4431-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4431-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4431-110">Prerequisites</span></span>
<span data-ttu-id="a4431-111">Per configurare l'integrazione di Azure AD con SciQuest Spend Director, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4431-111">To configure Azure AD integration with SciQuest Spend Director, you need the following items:</span></span>

* <span data-ttu-id="a4431-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4431-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a4431-113">Sottoscrizione di SciQuest Spend Director abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4431-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4431-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a4431-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a4431-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4431-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a4431-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a4431-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a4431-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4431-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="a4431-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a4431-118">Scenario Description</span></span>
<span data-ttu-id="a4431-119">L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a4431-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="a4431-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4431-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4431-121">Aggiunta di SciQuest Spend Director dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4431-121">Adding SciQuest Spend Director from the gallery</span></span> 
2. <span data-ttu-id="a4431-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4431-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-the-gallery"></a><span data-ttu-id="a4431-123">Aggiunta di SciQuest Spend Director dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="a4431-123">Adding SciQuest Spend Director from the gallery</span></span>
<span data-ttu-id="a4431-124">Per configurare l'integrazione di SciQuest Spend Director in Azure AD, è necessario aggiungere SciQuest Spend Director dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a4431-124">To configure the integration of SciQuest Spend Director into Azure AD, you need to add SciQuest Spend Director from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a4431-125">**Per aggiungere SciQuest Spend Director dalla raccolta, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4431-125">**To add SciQuest Spend Director from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a4431-126">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4431-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="a4431-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="a4431-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="a4431-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="a4431-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="a4431-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="a4431-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="a4431-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="a4431-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="a4431-135">Nella casella di ricerca digitare **sciQuest spend director**.</span><span class="sxs-lookup"><span data-stu-id="a4431-135">In the search box, type **sciQuest spend director**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="a4431-137">Nel riquadro dei risultati selezionare **SciQuest Spend Director**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4431-137">In the results pane, select **SciQuest Spend Director**, and then click **Complete** to add the application.</span></span>
   
    ![Applicazioni][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4431-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4431-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4431-140">L'obiettivo di questa sezione è illustrare come configurare e testare l'accesso Single Sign-On di Azure AD con SciQuest Spend Director in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a4431-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4431-141">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di SciQuest Spend Director che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4431-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SciQuest Spend Director to an user in Azure AD is.</span></span> <span data-ttu-id="a4431-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-142">In other words, a link relationship between an Azure AD user and the related user in SciQuest Spend Director needs to be established.</span></span>  
<span data-ttu-id="a4431-143">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **nome utente** in SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="a4431-144">Per configurare e testare l'accesso Single Sign-On di Azure AD con SciQuest Spend Director, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4431-144">To configure and test Azure AD single sign-on with SciQuest Spend Director, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a4431-145">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a4431-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a4431-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4431-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4431-147">**[Creazione di un utente test di SciQuest Spend Director](#creating-a-halogen-software-test-user)** : per avere una controparte di Britta Simon in SciQuest Spend Director collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4431-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in SciQuest Spend Director that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a4431-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4431-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4431-149">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="a4431-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="a4431-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4431-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="a4431-151">Questa sezione descrive come abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure classico e configurare l'accesso Single Sign-On nell'applicazione SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="a4431-152">**Per configurare Single Sign-On di Azure AD con SciQuest Spend Director, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4431-152">**To configure Azure AD single sign-on with SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="a4431-153">Nella pagina di integrazione dell'applicazione **SciQuest Spend Director** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4431-153">In the Azure classic portal, on the **SciQuest Spend Director** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][8]

2. <span data-ttu-id="a4431-155">Nella pagina **How would you like users to sign on to SciQuest Spend Director** (Stabilire come si desidera che gli utenti accedano a SciQuest Spend Director) selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4431-155">On the **How would you like users to sign on to SciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]

3. <span data-ttu-id="a4431-157">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4431-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configurare le impostazioni dell'app][10]
   
     <span data-ttu-id="a4431-159">a.</span><span class="sxs-lookup"><span data-stu-id="a4431-159">a.</span></span> <span data-ttu-id="a4431-160">Nella casella di testo **URL di accesso** digitare l'URL usato dagli utenti per accedere all'applicazione SciQuest Spend Director nel formato seguente: *https://.*sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="a4431-160">In the **Sign On URL** textbox, type your URL used by your users to sign on to your SciQuest Spend Director application using the following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="a4431-161">b.</span><span class="sxs-lookup"><span data-stu-id="a4431-161">b.</span></span> <span data-ttu-id="a4431-162">Nella casella di testo **URL di risposta** digitare lo stesso valore immesso nella casella di testo **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="a4431-162">In the **Reply URL** textbox, type the same value you have typed into the **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="a4431-163">c.</span><span class="sxs-lookup"><span data-stu-id="a4431-163">c.</span></span> <span data-ttu-id="a4431-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4431-164">Click **Next**.</span></span>

4. <span data-ttu-id="a4431-165">Nella pagina **Configure single sign-on at SciQuest Spend Director** (Configura accesso Single Sign-On in SciQuest Spend Director) fare clic su **Scarica metadati**, quindi salvare il file di metadati localmente nel computer.</span><span class="sxs-lookup"><span data-stu-id="a4431-165">On the **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![Cos'è Azure AD Connect][11]

5. <span data-ttu-id="a4431-167">Contattare il supporto tecnico di SciQuest per abilitare questo metodo di autenticazione usando i metadati scaricati.</span><span class="sxs-lookup"><span data-stu-id="a4431-167">Contact SciQuest support to enable this authentication method using the above downloaded metadata.</span></span>

6. <span data-ttu-id="a4431-168">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4431-168">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span> 
   
    ![Cos'è Azure AD Connect][15]

7. <span data-ttu-id="a4431-170">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="a4431-170">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4431-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4431-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4431-172">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a4431-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="a4431-173">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4431-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a4431-174">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4431-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Cos'è Azure AD Connect][100] 

2. <span data-ttu-id="a4431-176">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="a4431-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="a4431-177">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="a4431-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][101] 

4. <span data-ttu-id="a4431-179">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="a4431-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Cos'è Azure AD Connect][102] 

5. <span data-ttu-id="a4431-181">Nella pagina della finestra di dialogo **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4431-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Cos'è Azure AD Connect][103] 
   
    <span data-ttu-id="a4431-183">a.</span><span class="sxs-lookup"><span data-stu-id="a4431-183">a.</span></span> <span data-ttu-id="a4431-184">In **Tipo di utente** selezionare **Nuovo utente nell'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="a4431-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="a4431-185">b.</span><span class="sxs-lookup"><span data-stu-id="a4431-185">b.</span></span> <span data-ttu-id="a4431-186">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4431-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a4431-187">c.</span><span class="sxs-lookup"><span data-stu-id="a4431-187">c.</span></span> <span data-ttu-id="a4431-188">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4431-188">Click **Next**.</span></span>

6. <span data-ttu-id="a4431-189">Nella pagina della finestra di dialogo **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4431-189">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Cos'è Azure AD Connect][104] 
   
    <span data-ttu-id="a4431-191">a.</span><span class="sxs-lookup"><span data-stu-id="a4431-191">a.</span></span> <span data-ttu-id="a4431-192">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a4431-192">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="a4431-193">b.</span><span class="sxs-lookup"><span data-stu-id="a4431-193">b.</span></span> <span data-ttu-id="a4431-194">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4431-194">In the **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="a4431-195">c.</span><span class="sxs-lookup"><span data-stu-id="a4431-195">c.</span></span> <span data-ttu-id="a4431-196">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4431-196">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="a4431-197">d.</span><span class="sxs-lookup"><span data-stu-id="a4431-197">d.</span></span> <span data-ttu-id="a4431-198">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="a4431-198">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="a4431-199">e.</span><span class="sxs-lookup"><span data-stu-id="a4431-199">e.</span></span> <span data-ttu-id="a4431-200">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4431-200">Click **Next**.</span></span>

7. <span data-ttu-id="a4431-201">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="a4431-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Cos'è Azure AD Connect][105]  

8. <span data-ttu-id="a4431-203">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4431-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Cos'è Azure AD Connect][106]   
   
    <span data-ttu-id="a4431-205">a.</span><span class="sxs-lookup"><span data-stu-id="a4431-205">a.</span></span> <span data-ttu-id="a4431-206">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="a4431-206">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="a4431-207">b.</span><span class="sxs-lookup"><span data-stu-id="a4431-207">b.</span></span> <span data-ttu-id="a4431-208">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a4431-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="a4431-209">Creazione di un utente test di SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="a4431-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="a4431-210">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-210">The objective of this section is to create a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="a4431-211">È necessario contattare il team del supporto tecnico di SciQuest Spend Director e fornire i dettagli relativi all'account di test perché possa essere creato.</span><span class="sxs-lookup"><span data-stu-id="a4431-211">You need to contact your SciQuest Spend Director support team and provide them with the details about your test account to get it created.</span></span>

<span data-ttu-id="a4431-212">In alternativa, è anche possibile sfruttare il provisioning JIT, una funzionalità Single Sign-On supportata da SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="a4431-213">Se il provisioning JIT è abilitato, gli utenti vengono creati automaticamente da SciQuest Spend Director durante un tentativo di accesso Single Sign-ON, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="a4431-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="a4431-214">Questa funzionalità elimina la necessità di creare manualmente le controparti per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a4431-214">This feature eliminates the need to manually create single sign-on counterpart users.</span></span>

<span data-ttu-id="a4431-215">Per abilitare il provisioning JIT, è necessario contattare il team del supporto tecnico di SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-215">To get just-in-time provisioning enabled, you need to contact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a4431-216">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4431-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="a4431-217">In questa sezione viene descritto come abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SciQuest Spend Director.</span></span>

![Cos'è Azure AD Connect][200]

<span data-ttu-id="a4431-219">**Per assegnare Britta Simon a SciQuest Spend Director, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a4431-219">**To assign Britta Simon to SciQuest Spend Director, perform the following steps:**</span></span>

1. <span data-ttu-id="a4431-220">Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="a4431-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Cos'è Azure AD Connect][201]

2. <span data-ttu-id="a4431-222">Nell'elenco delle applicazioni selezionare **SciQuest Spend Director**.</span><span class="sxs-lookup"><span data-stu-id="a4431-222">In the applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Cos'è Azure AD Connect][202]

3. <span data-ttu-id="a4431-224">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="a4431-224">In the menu on the top, click **Users**.</span></span>
   
    ![Cos'è Azure AD Connect][203]

4. <span data-ttu-id="a4431-226">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a4431-226">In the Users list, select **Britta Simon**.</span></span>
   
    ![Cos'è Azure AD Connect][204]

5. <span data-ttu-id="a4431-228">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="a4431-228">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Cos'è Azure AD Connect][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a4431-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4431-230">Testing Single Sign-On</span></span>
<span data-ttu-id="a4431-231">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4431-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a4431-232">Quando si fa clic sul riquadro SciQuest Spend Director nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="a4431-232">When you click the SciQuest Spend Director tile in the Access Panel, you should get automatically signed-on to your SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4431-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a4431-233">Additional Resources</span></span>
* [<span data-ttu-id="a4431-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4431-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4431-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4431-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

