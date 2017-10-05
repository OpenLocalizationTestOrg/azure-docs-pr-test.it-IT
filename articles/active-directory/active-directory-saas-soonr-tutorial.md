---
title: 'Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Soonr Workplace.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="76051-103">Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="76051-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="76051-104">Questa esercitazione descrive l'integrazione di Soonr Workplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76051-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="76051-105">L'integrazione di Soonr Workplace con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="76051-106">È possibile controllare in Azure AD chi può accedere a Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="76051-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="76051-107">È possibile abilitare gli utenti per l'accesso automatico a Soonr Workplace (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76051-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="76051-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="76051-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76051-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76051-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76051-110">Prerequisites</span></span>

<span data-ttu-id="76051-111">Per configurare l'integrazione di Azure AD con Soonr Workplace, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="76051-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76051-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76051-113">Sottoscrizione di Soonr Workplace abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="76051-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="76051-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="76051-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="76051-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76051-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="76051-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="76051-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76051-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="76051-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="76051-118">Scenario description</span></span>
<span data-ttu-id="76051-119">L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="76051-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="76051-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76051-121">Aggiunta di Soonr Workplace dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="76051-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="76051-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="76051-123">Aggiunta di Soonr Workplace dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="76051-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="76051-124">Per configurare l'integrazione di Soonr Workplace in Azure AD, è necessario aggiungere Soonr Workplace dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="76051-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76051-125">**Per aggiungere Soonr Workplace dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="76051-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76051-126">Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="76051-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76051-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="76051-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="76051-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="76051-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="76051-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="76051-131">Click **Add** at the bottom of the page.</span></span>

    ![Applicazioni][3]

5. <span data-ttu-id="76051-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="76051-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Applicazioni][4]

6. <span data-ttu-id="76051-135">Nella casella di ricerca digitare **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="76051-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="76051-137">Nel riquadro dei risultati selezionare **Soonr Workplace**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="76051-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76051-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76051-140">Questa sezione descrive come configurare e testare l'accesso Single Sign-On di Azure AD con Soonr Workplace con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="76051-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76051-141">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Soonr Workplace che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76051-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="76051-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="76051-143">La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="76051-144">Per configurare e testare l'accesso Single Sign-On di Azure AD con Soonr Workplace, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76051-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="76051-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="76051-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76051-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76051-147">**[Creazione di un utente test di Soonr Workplace](#creating-a-soonr-workplace-test-user)** : per avere una controparte di Britta Simon in Soonr Workplace collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76051-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="76051-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76051-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76051-149">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="76051-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76051-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76051-151">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure classico e viene configurato l'accesso Single Sign-On nell'applicazione Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="76051-152">**Per configurare l'accesso Single Sign-On di Azure AD con Soonr Workplace, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="76051-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="76051-153">Nella pagina di integrazione dell'applicazione **Soonr Workplace** nel portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="76051-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configura accesso Single Sign-On][6] 

2. <span data-ttu-id="76051-155">Nella pagina **Stabilire come si desidera che gli utenti accedano a Soonr Workplace** selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76051-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="76051-157">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76051-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="76051-159">a.</span><span class="sxs-lookup"><span data-stu-id="76051-159">a.</span></span> <span data-ttu-id="76051-160">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="76051-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="76051-161">b.</span><span class="sxs-lookup"><span data-stu-id="76051-161">b.</span></span> <span data-ttu-id="76051-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76051-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76051-163">Si noti che questo non è il valore reale.</span><span class="sxs-lookup"><span data-stu-id="76051-163">Please note that this is not the real value.</span></span> <span data-ttu-id="76051-164">È necessario aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="76051-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="76051-165">Per ottenere tale valore, contattare il team di supporto di Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="76051-166">Nella pagina **Configura accesso Single Sign-On in Soonr Workplace** fare clic su **Download metadati** e quindi salvare il file nel computer:</span><span class="sxs-lookup"><span data-stu-id="76051-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="76051-168">Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il team di supporto di Soonr Workplace e fornire gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="76051-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="76051-169">•  File dei **metadati** scaricato</span><span class="sxs-lookup"><span data-stu-id="76051-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="76051-170">•  **URL dell'autorità di certificazione**</span><span class="sxs-lookup"><span data-stu-id="76051-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="76051-171">•  **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="76051-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="76051-172">•  **URL del servizio Single Sign-Out**</span><span class="sxs-lookup"><span data-stu-id="76051-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="76051-173">Questa applicazione è stata sostituita da <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> ed è possibile vedere <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">questa</a> esercitazione per la configurazione dell'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76051-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="76051-174">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76051-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Single Sign-On di Microsoft Azure AD][10]

7. <span data-ttu-id="76051-176">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="76051-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Single Sign-On di Microsoft Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76051-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="76051-179">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="76051-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Creare un utente di Azure AD][20]

<span data-ttu-id="76051-181">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="76051-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76051-182">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="76051-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="76051-184">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="76051-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="76051-185">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="76051-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76051-187">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="76051-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="76051-189">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76051-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="76051-191">a.</span><span class="sxs-lookup"><span data-stu-id="76051-191">a.</span></span> <span data-ttu-id="76051-192">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="76051-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="76051-193">b.</span><span class="sxs-lookup"><span data-stu-id="76051-193">b.</span></span> <span data-ttu-id="76051-194">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76051-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76051-195">c.</span><span class="sxs-lookup"><span data-stu-id="76051-195">c.</span></span> <span data-ttu-id="76051-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76051-196">Click **Next**.</span></span>

6.  <span data-ttu-id="76051-197">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76051-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="76051-199">a.</span><span class="sxs-lookup"><span data-stu-id="76051-199">a.</span></span> <span data-ttu-id="76051-200">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="76051-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="76051-201">b.</span><span class="sxs-lookup"><span data-stu-id="76051-201">b.</span></span> <span data-ttu-id="76051-202">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="76051-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="76051-203">c.</span><span class="sxs-lookup"><span data-stu-id="76051-203">c.</span></span> <span data-ttu-id="76051-204">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="76051-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="76051-205">d.</span><span class="sxs-lookup"><span data-stu-id="76051-205">d.</span></span> <span data-ttu-id="76051-206">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="76051-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="76051-207">e.</span><span class="sxs-lookup"><span data-stu-id="76051-207">e.</span></span> <span data-ttu-id="76051-208">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76051-208">Click **Next**.</span></span>

7. <span data-ttu-id="76051-209">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="76051-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="76051-211">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76051-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="76051-213">a.</span><span class="sxs-lookup"><span data-stu-id="76051-213">a.</span></span> <span data-ttu-id="76051-214">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="76051-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="76051-215">b.</span><span class="sxs-lookup"><span data-stu-id="76051-215">b.</span></span> <span data-ttu-id="76051-216">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="76051-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="76051-217">Creazione di un utente test di Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="76051-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="76051-218">Questa sezione descrive come creare un utente chiamato Britta Simon in Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="76051-219">Collaborare con il team di supporto di Soonr Workplace per creare un utente nella piattaforma.</span><span class="sxs-lookup"><span data-stu-id="76051-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="76051-220">È possibile generare il ticket di supporto per Soonr da <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">qui</a>.</span><span class="sxs-lookup"><span data-stu-id="76051-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="76051-221">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76051-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="76051-222">Questa sezione descrive come abilitare Britta Simon per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Assegna utente][200] 

<span data-ttu-id="76051-224">**Per assegnare Britta Simon a Soonr Workplace, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="76051-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="76051-225">Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="76051-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="76051-227">Selezionare **Soonr Workplace**dall'elenco di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="76051-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="76051-229">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="76051-229">In the menu on the top, click **Users**.</span></span>

    ![Assegna utente][203] 

1. <span data-ttu-id="76051-231">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="76051-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="76051-232">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="76051-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Assegna utente][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="76051-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="76051-234">Testing single sign-on</span></span>

<span data-ttu-id="76051-235">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="76051-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="76051-236">Quando si fa clic sul riquadro Soonr Workplace nel pannello di accesso, si accederà automaticamente all'applicazione Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="76051-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="76051-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="76051-237">Additional resources</span></span>

* [<span data-ttu-id="76051-238">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76051-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76051-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76051-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
