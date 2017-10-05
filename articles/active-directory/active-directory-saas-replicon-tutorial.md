---
title: 'Esercitazione: Integrazione di Azure Active Directory con Replicon | Documentazione Microsoft'
description: Informazioni su come usare Replicon con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="bdaed-103">Esercitazione: Integrazione di Azure Active Directory con Replicon</span><span class="sxs-lookup"><span data-stu-id="bdaed-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="bdaed-104">In questa esercitazione viene illustrata l'integrazione di Azure e Replicon.</span><span class="sxs-lookup"><span data-stu-id="bdaed-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="bdaed-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="bdaed-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="bdaed-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="bdaed-106">A valid Azure subscription</span></span>
* <span data-ttu-id="bdaed-107">Tenant Replicon</span><span class="sxs-lookup"><span data-stu-id="bdaed-107">A Replicon tenant</span></span>

<span data-ttu-id="bdaed-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Replicon saranno in grado di eseguire l’accesso Single Sign-On all'applicazione tramite il sito aziendale di Replicon (accesso avviato dal provider di servizi) o seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdaed-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="bdaed-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdaed-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="bdaed-110">Abilitazione dell'integrazione dell'applicazione per Replicon</span><span class="sxs-lookup"><span data-stu-id="bdaed-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="bdaed-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="bdaed-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="bdaed-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="bdaed-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="bdaed-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="bdaed-113">Assigning users</span></span>

<span data-ttu-id="bdaed-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="bdaed-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="bdaed-115">Abilitare l'integrazione dell'applicazione per Replicon</span><span class="sxs-lookup"><span data-stu-id="bdaed-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="bdaed-116">In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per Replicon.</span><span class="sxs-lookup"><span data-stu-id="bdaed-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="bdaed-117">**Per abilitare l'integrazione dell'applicazione per Replicon, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bdaed-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="bdaed-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="bdaed-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="bdaed-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="bdaed-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="bdaed-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="bdaed-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bdaed-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="bdaed-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="bdaed-122">![Applicazioni](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="bdaed-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="bdaed-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="bdaed-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="bdaed-124">![Aggiungere un'applicazione](./media/active-directory-saas-replicon-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="bdaed-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="bdaed-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="bdaed-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-replicon-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="bdaed-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="bdaed-127">Nella **casella di ricerca** digitare **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="bdaed-128">![Raccolta di applicazioni](./media/active-directory-saas-replicon-tutorial/IC777799.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="bdaed-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="bdaed-129">Nel riquadro dei risultati selezionare **Replicon**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdaed-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="bdaed-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="bdaed-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="bdaed-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bdaed-131">Configure single sign-on</span></span>

<span data-ttu-id="bdaed-132">In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a Replicon tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="bdaed-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="bdaed-133">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bdaed-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="bdaed-134">Nella pagina di integrazione dell'applicazione **Replicon** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="bdaed-135">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bdaed-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="bdaed-136">Nella pagina **Stabilire come si desidera che gli utenti accedano a Replicon** selezionare **Single Sign-On di Microsoft Azure AD**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="bdaed-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bdaed-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="bdaed-138">Nella pagina **Configura URL app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="bdaed-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="bdaed-139">![Configurare l'URL dell'app](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="bdaed-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="bdaed-140">Nella casella di testo dell'**URL di accesso a Replicon** digitare l'URL del tenant Replicon (ad esempio: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="bdaed-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="bdaed-141">Nella casella di testo **Replicon Reply URL** (URL di risposta Replicon) digitare l'URL **AssertionConsumerService** di Replicon, ad esempio *https://global.replicon.com/!/saml2/company/sso/post*.</span><span class="sxs-lookup"><span data-stu-id="bdaed-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="bdaed-142">È possibile ottenere l'URL dai metadati Replicon in: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="bdaed-143">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-143">Click **Next**.</span></span>

4. <span data-ttu-id="bdaed-144">Nella pagina **Configura accesso Single Sign-On in Replicon** fare clic su **Scarica metadati** per scaricare il file di metadati e salvare i metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="bdaed-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="bdaed-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bdaed-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="bdaed-146">In un'altra finestra del Web browser accedere al sito aziendale di Replicon come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bdaed-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="bdaed-147">Per configurare SAML 2.0, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bdaed-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="bdaed-148">![Abilita autenticazione SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "autenticazione SAML abilitare")</span><span class="sxs-lookup"><span data-stu-id="bdaed-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="bdaed-149">Per visualizzare la finestra di dialogo **EnableSAMLAuthentication2** aggiungere quanto segue all'URL, dopo la chiave dell'azienda: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="bdaed-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="bdaed-150">Di seguito è illustrato lo schema dell'URL completo:</span><span class="sxs-lookup"><span data-stu-id="bdaed-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="bdaed-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="bdaed-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="bdaed-152">Fare clic su **+** per espandere la sezione **v20Configuration**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="bdaed-153">Fare clic su **+** per espandere la sezione **metaDataConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="bdaed-154">Fare clic su **Scegli file** per selezionare il file XML dei metadati del provider di identità, quindi scegliere **Invia**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="bdaed-155">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="bdaed-156">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bdaed-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="bdaed-157">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bdaed-157">Configure user provisioning</span></span>

<span data-ttu-id="bdaed-158">Per consentire agli utenti di Azure AD di accedere a Replicon, è necessario eseguirne il provisioning in Replicon.</span><span class="sxs-lookup"><span data-stu-id="bdaed-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="bdaed-159">Nel caso di Replicon, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="bdaed-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="bdaed-160">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bdaed-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="bdaed-161">In una finestra del Web browser accedere al sito aziendale di Replicon come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bdaed-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="bdaed-162">Passare ad **Amministrazione \> Utenti**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="bdaed-163">![Utenti](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="bdaed-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="bdaed-164">Fare clic su **+Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="bdaed-165">![Aggiungere un utente](./media/active-directory-saas-replicon-tutorial/IC777807.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="bdaed-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="bdaed-166">Nella sezione **Profilo utente** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bdaed-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="bdaed-167">![Profilo utente](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profilo utente")</span><span class="sxs-lookup"><span data-stu-id="bdaed-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="bdaed-168">Nella casella di testo **Nome accesso** , digitare l’indirizzo di posta elettronica dell'utente di Azure AD di cui si desidera eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="bdaed-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="bdaed-169">In **Tipo di autenticazione** selezionare **SSO**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="bdaed-170">Nella casella di testo **Reparto** , digitare il reparto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bdaed-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="bdaed-171">In **Tipo di dipendente** selezionare **Amministratore**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="bdaed-172">Fare clic su **Salva profilo utente**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="bdaed-173">È possibile usare qualsiasi altro strumento o API di creazione di account utente offerti da Replicon per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdaed-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="bdaed-174">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="bdaed-174">Assign users</span></span>
<span data-ttu-id="bdaed-175">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bdaed-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="bdaed-176">**Per assegnare gli utenti a Replicon, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="bdaed-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="bdaed-177">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="bdaed-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="bdaed-178">Nella pagina di integrazione dell'applicazione **Replicon** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="bdaed-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="bdaed-179">![Assegnare utenti](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="bdaed-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="bdaed-180">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="bdaed-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="bdaed-181">![Sì](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="bdaed-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="bdaed-182">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bdaed-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="bdaed-183">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bdaed-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

