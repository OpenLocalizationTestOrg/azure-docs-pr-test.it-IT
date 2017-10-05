---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Wizergos Productivity Software.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="bb6cb-103">Esercitazione: Integrazione di Azure Active Directory con Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="bb6cb-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="bb6cb-104">Questa esercitazione descrive l'integrazione di Wizergos Productivity Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb6cb-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb6cb-105">L'integrazione di Wizergos Productivity Software con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="bb6cb-106">È possibile controllare in Azure AD chi può accedere a Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="bb6cb-107">È possibile abilitare gli utenti per l'accesso Single Sign-On automatico a Wizergos Productivity Software (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="bb6cb-108">È possibile gestire gli account da una posizione centrale: il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="bb6cb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="bb6cb-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb6cb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb6cb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb6cb-110">Prerequisites</span></span>
<span data-ttu-id="bb6cb-111">Per configurare l'integrazione di Azure AD con Wizergos Productivity Software, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="bb6cb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="bb6cb-113">Sottoscrizione di Wizergos Productivity Software abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="bb6cb-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="bb6cb-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="bb6cb-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bb6cb-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bb6cb-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb6cb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb6cb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bb6cb-118">Scenario description</span></span>
<span data-ttu-id="bb6cb-119">L'obiettivo di questa esercitazione è quello di testare l'accesso Single Sign-On (SSO) di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="bb6cb-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb6cb-121">Aggiunta di Wizergos Productivity Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bb6cb-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="bb6cb-122">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="bb6cb-123">Aggiunta di Wizergos Productivity Software dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="bb6cb-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="bb6cb-124">Per configurare l'integrazione di Wizergos Productivity Software in Azure AD, è necessario aggiungere Wizergos Productivity Software dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bb6cb-125">**Per aggiungere Wizergos Productivity Software dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bb6cb-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bb6cb-126">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="bb6cb-128">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bb6cb-129">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="bb6cb-131">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applicazioni][3]
5. <span data-ttu-id="bb6cb-133">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applicazioni][4]
6. <span data-ttu-id="bb6cb-135">Nella casella di ricerca digitare **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="bb6cb-137">Nel pannello dei risultati selezionare **Wizergos Productivity Software** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Selezione dell'app nella raccolta](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="bb6cb-139">Configurare e testare l'accesso Single Sign-On (SSO) di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="bb6cb-140">Questa sezione descrive come configurare e testare l'accesso SSO di Azure AD con Wizergos Productivity Software con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb6cb-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb6cb-141">Per il funzionamento dell'accesso SSO, Azure AD deve conoscere qual è l'utente di Wizergos Productivity Software che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="bb6cb-142">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="bb6cb-143">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="bb6cb-144">Per configurare e testare l'accesso Single Sign-On di Azure AD con Wizergos Productivity Software, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bb6cb-145">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bb6cb-146">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb6cb-147">**[Creazione di un utente di test Wizergos Productivity Software](#creating-a-wizergos-productivity-software-test-user)** : per avere una controparte di Britta Simon in Wizergos Productivity Software collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="bb6cb-148">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb6cb-149">**[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="bb6cb-150">Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="bb6cb-151">In questa sezione nel portale classico viene abilitato l'accesso Single Sign-On di Azure AD, che viene configurato nell'applicazione Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="bb6cb-152">**Per configurare Single Sign-On di Azure AD con Wizergos Productivity Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bb6cb-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="bb6cb-153">Nella pagina di integrazione dell'applicazione **Wizergos Productivity Software** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 
2. <span data-ttu-id="bb6cb-155">Nella pagina **Stabilire come si desidera che gli utenti accedano a Wizergos Productivity Software** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="bb6cb-157">Nella pagina **Configurare le impostazioni dell'app** fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="bb6cb-159">Nella pagina **Configura accesso Single Sign-On in Wizergos Productivity Software** fare clic su **Scarica certificato** e quindi salvare il file nel computer:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="bb6cb-161">In un'altra finestra del browser Web accedere al tenant Wizergos Productivity Software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="bb6cb-162">Dal menu hamburger, selezionare **Admin**(Amministratore).</span><span class="sxs-lookup"><span data-stu-id="bb6cb-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="bb6cb-164">Nella pagina visualizzata selezionare **AUTHENTICATION** (AUTENTICAZIONE) nel menu a sinistra e fare clic su **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="bb6cb-166">Seguire questa procedura nella sezione **AUTHENTICATION** (AUTENTICAZIONE).</span><span class="sxs-lookup"><span data-stu-id="bb6cb-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="bb6cb-168">Fare clic sull'icona **UPLOAD** (CARICA) per caricare il certificato scaricato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="bb6cb-169">Nella casella di testo **Issuer URL** (URL autorità di certificazione) inserire il valore di **URL autorità di certificazione** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="bb6cb-170">Nella casella di testo **Single Sign-On URL** (URL Single Sign-On) inserire il valore di **URL servizio Single Sign-On** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="bb6cb-171">Nella casella di testo **Single Sign-Out URL** (URL Single Sign-Out) inserire il valore di **URL servizio Single Sign-Out** dalla configurazione guidata dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="bb6cb-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bb6cb-172">Click **Save** button.</span></span>
9. <span data-ttu-id="bb6cb-173">Nel portale di Azure classico selezionare la conferma della configurazione e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][10]
10. <span data-ttu-id="bb6cb-175">Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bb6cb-177">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-177">Create an Azure AD test user</span></span>
<span data-ttu-id="bb6cb-178">Questa sezione descrive come creare un utente di test chiamato Britta Simon nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="bb6cb-180">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bb6cb-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bb6cb-181">Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="bb6cb-183">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bb6cb-184">Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="bb6cb-186">Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="bb6cb-188">Nella pagina **Informazioni sull'utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="bb6cb-190">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="bb6cb-191">Nella casella di testo **Nome utente** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="bb6cb-192">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-192">Click **Next**.</span></span>
6. <span data-ttu-id="bb6cb-193">Nella pagina **Profilo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="bb6cb-195">Nella casella di testo **Nome** digitare **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="bb6cb-196">Nella casella di testo **Cognome** digitare **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="bb6cb-197">Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="bb6cb-198">Nell'elenco **Ruolo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="bb6cb-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-199">Click **Next**.</span></span>
7. <span data-ttu-id="bb6cb-200">Nella pagina **Ottieni password temporanea** fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="bb6cb-202">Nella pagina **Ottieni password temporanea** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bb6cb-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="bb6cb-204">Prendere nota del valore visualizzato in **Nuova password**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="bb6cb-205">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="bb6cb-206">Creare un utente di test Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="bb6cb-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="bb6cb-207">In questa sezione viene creato un utente chiamato Britta Simon in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="bb6cb-208">Per aggiungere utenti alla piattaforma di Wizergos Productivity Software, collaborare con il team di Wizergos Productivity Software tramite l'indirizzo [support@wizergos.com](emailTo:support@wizergos.com) .</span><span class="sxs-lookup"><span data-stu-id="bb6cb-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bb6cb-209">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb6cb-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="bb6cb-210">Questa sezione descrive come abilitare Britta Simon per l'uso dell'accesso SSO di Azure concedendole l'accesso a Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Assegna utente][200]

<span data-ttu-id="bb6cb-212">**Per assegnare Britta Simon a Wizergos Productivity Software, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bb6cb-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="bb6cb-213">Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione Directory fare clic su **Applicazioni** nel menu in alto.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assegna utente][201]
2. <span data-ttu-id="bb6cb-215">Nell'elenco di applicazioni selezionare **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="bb6cb-217">Scegliere **Utenti**dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-217">In the menu on the top, click **Users**.</span></span>
   
    ![Assegna utente][203]
4. <span data-ttu-id="bb6cb-219">Nell'elenco di utenti selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="bb6cb-220">Fare clic su **Assegna**sulla barra degli strumenti in basso.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="bb6cb-222">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bb6cb-222">Test single sign-on</span></span>
<span data-ttu-id="bb6cb-223">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bb6cb-224">Quando si fa clic sul riquadro Wizergos Productivity Software nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="bb6cb-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb6cb-225">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bb6cb-225">Additional resources</span></span>
* [<span data-ttu-id="bb6cb-226">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb6cb-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb6cb-227">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb6cb-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
