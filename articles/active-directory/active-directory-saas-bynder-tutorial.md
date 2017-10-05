---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bynder | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Bynder.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="eeb57-103">Esercitazione: Integrazione di Azure Active Directory con Bynder</span><span class="sxs-lookup"><span data-stu-id="eeb57-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="eeb57-104">Questa esercitazione descrive l'integrazione di Bynder con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eeb57-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eeb57-105">L'integrazione di Bynder con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeb57-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="eeb57-106">È possibile controllare in Azure AD chi può accedere a Bynder</span><span class="sxs-lookup"><span data-stu-id="eeb57-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="eeb57-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On (SSO) a Bynder con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="eeb57-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="eeb57-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="eeb57-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eeb57-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eeb57-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eeb57-110">Prerequisites</span></span>
<span data-ttu-id="eeb57-111">Per configurare l'integrazione di Azure AD con Bynder, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeb57-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="eeb57-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeb57-112">An Azure AD subscription</span></span>
* <span data-ttu-id="eeb57-113">Sottoscrizione di Bynder abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="eeb57-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="eeb57-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="eeb57-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="eeb57-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeb57-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="eeb57-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="eeb57-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="eeb57-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeb57-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eeb57-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="eeb57-118">Scenario description</span></span>
<span data-ttu-id="eeb57-119">L'obiettivo di questa esercitazione è quello di testare l'accesso Single Sign-On (SSO) di Microsoft Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="eeb57-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="eeb57-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeb57-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eeb57-121">Aggiunta di Bynder dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eeb57-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="eeb57-122">Configurazione e test dell'accesso Single Sign-On di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="eeb57-123">Aggiungere Bynder dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="eeb57-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="eeb57-124">Per configurare l'integrazione di Bynder in Azure AD, è necessario aggiungere Bynder dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="eeb57-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eeb57-125">**Per aggiungere Bynder dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eeb57-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eeb57-126">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eeb57-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="eeb57-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="eeb57-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="eeb57-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="eeb57-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="eeb57-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="eeb57-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="eeb57-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="eeb57-135">Nella casella di ricerca digitare **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-135">In the search box, type **Bynder**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="eeb57-137">Nel riquadro dei risultati selezionare **Bynder** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eeb57-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Selezione dell'app nella raccolta](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="eeb57-139">Configurare e testare l'accesso Single Sign-On di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="eeb57-140">Questa sezione descrive come configurare e testare l'accesso Single Sign-On di Microsoft Azure AD con Bynder in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eeb57-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eeb57-141">Per il funzionamento dell'accesso SSO, Azure AD deve conoscere qual è l'utente di Bynder che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeb57-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="eeb57-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="eeb57-143">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="eeb57-144">Per configurare e testare l'accesso Single Sign-On di Microsoft Azure AD con Bynder, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eeb57-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eeb57-145">**[Configurazione dell'accesso Single Sign-On di Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="eeb57-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eeb57-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Microsoft Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eeb57-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="eeb57-147">**[Creazione di un utente test Bynder](#creating-a-bynder-test-user)** : per avere una controparte di Britta Simon in Bynder collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeb57-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="eeb57-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eeb57-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="eeb57-149">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="eeb57-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="eeb57-150">Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="eeb57-151">In questa sezione viene abilitato l'accesso SSO di Microsoft Azure AD nel portale classico e viene configurato l'accesso SSO nell'applicazione Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="eeb57-152">**Per configurare SSO di Microsoft Azure AD con Bynder, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eeb57-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="eeb57-153">Nella pagina di integrazione dell'applicazione **Bynder** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="eeb57-155">Nella pagina **Stabilire come si desidera che gli utenti accedano a Bynder** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="eeb57-157">Nella pagina della finestra di dialogo **Configurare le impostazioni dell'app**, se si desidera configurare l'applicazione in **modalità iniziata da IDP**,seguire la procedura seguente e fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="eeb57-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="eeb57-159">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="eeb57-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="eeb57-160">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-160">Click **Next**.</span></span>
4. <span data-ttu-id="eeb57-161">Se si desidera configurare l'applicazione in **SP initiated mode** (Modalità iniziata dal provider di servizi) nella finestra di dialogo **Configurare le impostazioni dell'app** fare clic su **"Mostra opzioni avanzate (facoltativo)"**, quindi digitare l'**URL di accesso** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="eeb57-163">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="eeb57-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="eeb57-164">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="eeb57-165">Il valore dell'URL di accesso in questa esercitazione è solo un segnaposto.</span><span class="sxs-lookup"><span data-stu-id="eeb57-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="eeb57-166">Per ottenere il valore effettivo per l'ambiente, contattare Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="eeb57-167">Nella pagina **Configura accesso Single Sign-On in Bynder** seguire questa procedura e fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="eeb57-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="eeb57-169">Fare clic su **Scarica metadati**e quindi salvare il file nel computer.</span><span class="sxs-lookup"><span data-stu-id="eeb57-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="eeb57-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-170">Click **Next**.</span></span>
6. <span data-ttu-id="eeb57-171">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il team di supporto Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="eeb57-172">Allegare il file dei metadati scaricato e condividerlo con il team Bynder per la configurazione di SSO sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="eeb57-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="eeb57-173">Nel portale classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][10]
8. <span data-ttu-id="eeb57-175">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eeb57-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-177">Create an Azure AD test user</span></span>
<span data-ttu-id="eeb57-178">Questa sezione descrive come creare un utente di test chiamato Britta Simon nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="eeb57-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="eeb57-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="eeb57-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eeb57-181">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="eeb57-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="eeb57-183">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="eeb57-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="eeb57-184">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eeb57-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="eeb57-186">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="eeb57-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="eeb57-188">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eeb57-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="eeb57-190">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eeb57-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="eeb57-191">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="eeb57-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-192">Click **Next**.</span></span>
6. <span data-ttu-id="eeb57-193">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eeb57-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="eeb57-195">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="eeb57-196">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="eeb57-197">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="eeb57-198">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="eeb57-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-199">Click **Next**.</span></span>
7. <span data-ttu-id="eeb57-200">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="eeb57-202">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eeb57-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="eeb57-204">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="eeb57-205">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="eeb57-206">Creare un utente test per Bynder</span><span class="sxs-lookup"><span data-stu-id="eeb57-206">Create a Bynder test user</span></span>
<span data-ttu-id="eeb57-207">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="eeb57-208">Bynder supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="eeb57-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="eeb57-209">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eeb57-209">There is no action item for you in this section.</span></span> <span data-ttu-id="eeb57-210">Durante un tentativo di accesso a Bynder verrà creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="eeb57-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="eeb57-211">Per creare un utente manualmente, è necessario contattare il team di supporto di Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eeb57-212">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="eeb57-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="eeb57-213">Questa sezione descrive come abilitare Britta Simon all'uso dell'accesso SSO di Azure concedendole l'accesso a Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Assegna utente][200]

<span data-ttu-id="eeb57-215">**Per assegnare Britta Simon a Bynder, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="eeb57-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="eeb57-216">Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eeb57-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][201]
2. <span data-ttu-id="eeb57-218">Nell'elenco delle applicazioni, selezionare **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-218">In the applications list, select **Bynder**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="eeb57-220">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="eeb57-220">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][203]
4. <span data-ttu-id="eeb57-222">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="eeb57-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="eeb57-223">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="eeb57-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="eeb57-225">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eeb57-225">Test single sign-on</span></span>
<span data-ttu-id="eeb57-226">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Microsoft Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="eeb57-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="eeb57-227">Quando si fa clic sul riquadro Bynder nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Bynder.</span><span class="sxs-lookup"><span data-stu-id="eeb57-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeb57-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eeb57-228">Additional resources</span></span>
* [<span data-ttu-id="eeb57-229">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eeb57-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eeb57-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eeb57-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
