---
title: 'Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Splunk Enterprise e Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="05bbb-103">Esercitazione: Integrazione di Azure Active Directory con Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="05bbb-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="05bbb-104">Questa esercitazione descrive come integrare Splunk Enterprise e Splunk Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05bbb-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05bbb-105">L'integrazione di Splunk Enterprise e Splunk Cloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05bbb-106">È possibile controllare in Azure AD chi può accedere a Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="05bbb-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="05bbb-107">È possibile abilitare gli utenti per l'accesso automatico a Splunk Enterprise e Splunk Cloud Single Sign-On (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="05bbb-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="05bbb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="05bbb-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05bbb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05bbb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05bbb-110">Prerequisites</span></span>

<span data-ttu-id="05bbb-111">Per configurare l'integrazione di Azure AD con Splunk Enterprise e Splunk Cloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="05bbb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05bbb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05bbb-113">Sottoscrizione di Splunk Enterprise o Splunk Cloud abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="05bbb-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="05bbb-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="05bbb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="05bbb-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05bbb-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="05bbb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="05bbb-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05bbb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="05bbb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="05bbb-118">Scenario description</span></span>
<span data-ttu-id="05bbb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="05bbb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="05bbb-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05bbb-121">Aggiunta di Splunk Enterprise e Splunk Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="05bbb-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="05bbb-122">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="05bbb-123">Aggiungere Splunk Enterprise e Splunk Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="05bbb-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="05bbb-124">Per configurare l'integrazione di Splunk Enterprise e Splunk Cloud in Azure AD, è necessario aggiungere Splunk Enterprise e Splunk Cloud dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="05bbb-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05bbb-125">**Per aggiungere Splunk Enterprise e Splunk Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="05bbb-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05bbb-126">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="05bbb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="05bbb-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="05bbb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="05bbb-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="05bbb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="05bbb-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="05bbb-131">Click **Add** at the bottom of the page.</span></span>

    ![Applicazioni][3]

5. <span data-ttu-id="05bbb-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applicazioni][4]

6. <span data-ttu-id="05bbb-135">Nella casella di ricerca digitare **Splunk Enterprise o Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="05bbb-137">Nel pannello dei risultati selezionare **Splunk Enterprise e Splunk Cloud** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="05bbb-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="05bbb-139">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="05bbb-140">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="05bbb-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05bbb-141">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Splunk Enterprise e Splunk Cloud che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05bbb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="05bbb-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="05bbb-143">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="05bbb-144">Per configurare e testare l'accesso Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05bbb-145">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="05bbb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05bbb-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05bbb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05bbb-147">**[Creazione di un utente test di Splunk Enterprise e Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**: per avere una controparte di Britta Simon in Splunk Enterprise e Splunk Cloud collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05bbb-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="05bbb-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05bbb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05bbb-149">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="05bbb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="05bbb-150">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="05bbb-151">In questa sezione viene abilitato l'accesso SSO di Azure AD nel portale di Azure classico e viene configurato l'accesso SSO nell'applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="05bbb-152">**Per configurare Single Sign-On di Azure AD con Splunk Enterprise e Splunk Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="05bbb-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="05bbb-153">Nella pagina di integrazione dell'applicazione **Splunk Enterprise e Splunk Cloud** del portale classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configura accesso Single Sign-On][6] 

2. <span data-ttu-id="05bbb-155">Nella pagina **Stabilire come si desidera che gli utenti accedano a Splunk Enterprise e Splunk Cloud** selezionare **Accesso Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="05bbb-157">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="05bbb-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="05bbb-159">Nella casella di testo **URL di accesso** digitare l'URL usato dagli utenti per accedere all'applicazione Splunk Enterprise e Splunk Cloud adottando il modello seguente: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="05bbb-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="05bbb-160">Nella casella di testo **Identificatore** digitare l'URL del server Splunk.</span><span class="sxs-lookup"><span data-stu-id="05bbb-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="05bbb-161">Nella casella di testo **URL di risposta** digitare l'URL nel formato seguente: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="05bbb-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="05bbb-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="05bbb-163">Nella pagina **Configura accesso Single Sign-On in Splunk Enterprise e Splunk Cloud** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="05bbb-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="05bbb-165">Fare clic su **Scarica metadati**e quindi salvare il file nel computer.</span><span class="sxs-lookup"><span data-stu-id="05bbb-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="05bbb-166">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-166">Click **Next**.</span></span>

5. <span data-ttu-id="05bbb-167">Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il team di supporto di Splunk Enterprise e Splunk Cloud e fornire gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="05bbb-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="05bbb-168">I **metadati della federazione** scaricati.</span><span class="sxs-lookup"><span data-stu-id="05bbb-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="05bbb-169">Nel portale classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. <span data-ttu-id="05bbb-171">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="05bbb-173">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-173">Create an Azure AD test user</span></span>
<span data-ttu-id="05bbb-174">In questa sezione viene creato un utente test chiamato Britta Simon nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="05bbb-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="05bbb-176">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="05bbb-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05bbb-177">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="05bbb-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="05bbb-179">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="05bbb-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="05bbb-180">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="05bbb-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05bbb-182">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="05bbb-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="05bbb-184">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="05bbb-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="05bbb-186">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="05bbb-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="05bbb-187">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="05bbb-188">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-188">Click **Next**.</span></span>

6.  <span data-ttu-id="05bbb-189">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="05bbb-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="05bbb-191">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="05bbb-192">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="05bbb-193">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="05bbb-194">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="05bbb-195">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-195">Click **Next**.</span></span>

7. <span data-ttu-id="05bbb-196">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="05bbb-198">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="05bbb-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="05bbb-200">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="05bbb-201">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="05bbb-202">Creare un utente test di Splunk Enterprise e Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="05bbb-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="05bbb-203">In questa sezione viene creato un utente chiamato Britta Simon in Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="05bbb-204">Rivolgersi al team di supporto di Splunk Enterprise e Splunk Cloud per aggiungere gli utenti nella piattaforma Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="05bbb-205">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="05bbb-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="05bbb-206">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso SSO di Azure concedendole l'accesso a Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="05bbb-208">**Per assegnare Britta Simon a Splunk Enterprise e Splunk Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="05bbb-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="05bbb-209">Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="05bbb-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="05bbb-211">Nell'elenco delle applicazioni selezionare **Splunk Enterprise e Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="05bbb-213">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="05bbb-213">In the menu on the top, click **Users**.</span></span>

    ![Assegna utente][203]

4. <span data-ttu-id="05bbb-215">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05bbb-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="05bbb-216">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="05bbb-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="05bbb-218">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05bbb-218">Test single sign-on</span></span>

<span data-ttu-id="05bbb-219">In questa sezione viene testata la configurazione dell'accesso SSO di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="05bbb-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="05bbb-220">Quando si fa clic sul riquadro Splunk Enterprise e Splunk Cloud nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Splunk Enterprise e Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="05bbb-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="05bbb-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="05bbb-221">Additional resources</span></span>

* [<span data-ttu-id="05bbb-222">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05bbb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05bbb-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05bbb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
