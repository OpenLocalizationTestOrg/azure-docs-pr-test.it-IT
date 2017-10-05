---
title: 'Esercitazione: Integrazione di Azure Active Directory con Benefitsolver | Microsoft Docs'
description: Informazioni su come usare Benefitsolver con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="406fe-103">Esercitazione: Integrazione di Azure Active Directory con Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="406fe-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="406fe-104">Questa esercitazione descrive l'integrazione di Azure e Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="406fe-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="406fe-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="406fe-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="406fe-106">A valid Azure subscription</span></span>
* <span data-ttu-id="406fe-107">Sottoscrizione di Benefitsolver abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="406fe-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="406fe-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Benefitsolver potranno eseguire l'accesso Single Sign-On all'applicazione seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="406fe-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="406fe-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="406fe-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="406fe-110">Abilitazione dell'integrazione dell'applicazione per Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="406fe-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="406fe-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="406fe-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="406fe-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="406fe-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="406fe-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="406fe-113">Assigning users</span></span>

<span data-ttu-id="406fe-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="406fe-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="406fe-115">Abilitazione dell'integrazione dell'applicazione per Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="406fe-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="406fe-116">Questa sezione descrive come abilitare l'integrazione dell'applicazione per Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="406fe-117">Per abilitare l'integrazione dell'applicazione per Benefitsolver, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="406fe-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="406fe-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="406fe-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="406fe-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="406fe-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="406fe-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="406fe-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="406fe-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="406fe-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="406fe-122">![Applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="406fe-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="406fe-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="406fe-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="406fe-124">![Aggiungere un'applicazione](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="406fe-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="406fe-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="406fe-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="406fe-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="406fe-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="406fe-127">Nella **casella di ricerca** digitare **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="406fe-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="406fe-128">![Raccolta di applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="406fe-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="406fe-129">Nel riquadro dei risultati selezionare **Benefitsolver** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="406fe-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="406fe-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="406fe-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="406fe-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="406fe-131">Configure single sign-on</span></span>

<span data-ttu-id="406fe-132">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a Benefitsolver tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="406fe-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="406fe-133">L'applicazione Benefitsolver prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione di **Attributi token SAML**.</span><span class="sxs-lookup"><span data-stu-id="406fe-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="406fe-134">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="406fe-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="406fe-135">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="406fe-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="406fe-136">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="406fe-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="406fe-137">Nella pagina di integrazione dell'applicazione **Benefitsolver** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="406fe-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="406fe-138">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="406fe-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="406fe-139">Nella pagina **Stabilire come si desidera che gli utenti accedano a Benefitsolver** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="406fe-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="406fe-140">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="406fe-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="406fe-141">Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="406fe-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="406fe-142">![Configurare le impostazioni dell'app](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurare le impostazioni dell'app")</span><span class="sxs-lookup"><span data-stu-id="406fe-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="406fe-143">Nella casella di testo **URL di accesso** digitare **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="406fe-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="406fe-144">Nella casella di testo **URL di risposta** digitare **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="406fe-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="406fe-145">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="406fe-145">Click **Next**.</span></span>
4. <span data-ttu-id="406fe-146">Nella pagina **Configura accesso Single Sign-On in Benefitsolver** fare clic su **Download metadati** per scaricare il file di metadati e quindi salvarlo nel computer.</span><span class="sxs-lookup"><span data-stu-id="406fe-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="406fe-147">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="406fe-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="406fe-148">Inviare il file di metadati scaricato al team di supporto di Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="406fe-149">Il team di supporto di Benefitsolver si occuperà dell'effettiva configurazione dell'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="406fe-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="406fe-150">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="406fe-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="406fe-151">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="406fe-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="406fe-152">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="406fe-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="406fe-153">Nel menu in alto fare clic su **Attributi** to open the **SAML Token Attributi** .</span><span class="sxs-lookup"><span data-stu-id="406fe-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="406fe-154">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="406fe-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="406fe-155">Per aggiungere i mapping di attributi obbligatori, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="406fe-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="406fe-156">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="406fe-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="406fe-157">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="406fe-157">Attribute Name</span></span> | <span data-ttu-id="406fe-158">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="406fe-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="406fe-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="406fe-159">ClientID</span></span> |<span data-ttu-id="406fe-160">È necessario ottenere questo valore dal team di supporto di Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="406fe-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="406fe-161">ClientKey</span></span> |<span data-ttu-id="406fe-162">È necessario ottenere questo valore dal team di supporto di Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="406fe-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="406fe-163">LogoutURL</span></span> |<span data-ttu-id="406fe-164">È necessario ottenere questo valore dal team di supporto di Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="406fe-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="406fe-165">EmployeeID</span></span> |<span data-ttu-id="406fe-166">È necessario ottenere questo valore dal team di supporto di Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="406fe-167">Per ogni riga di dati nella tabella precedente, fare clic su **aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="406fe-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="406fe-168">Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.</span><span class="sxs-lookup"><span data-stu-id="406fe-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="406fe-169">Nella casella di testo **Valore attributo** , selezionare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="406fe-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="406fe-170">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="406fe-170">Click **Complete**.</span></span>
9. <span data-ttu-id="406fe-171">Fare clic su **Applica modifiche**.</span><span class="sxs-lookup"><span data-stu-id="406fe-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="406fe-172">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="406fe-172">Configure user provisioning</span></span>
<span data-ttu-id="406fe-173">Per consentire agli utenti di Azure AD di accedere a Benefitsolver, è necessario eseguirne il provisioning in Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="406fe-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="406fe-174">Nel caso di Benefitsolver, i dati dei dipendenti si trovano nell'applicazione popolata tramite un file di censimento del sistema HRIS, in genere durante la notte.</span><span class="sxs-lookup"><span data-stu-id="406fe-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="406fe-175">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Benefitsolver per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="406fe-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="406fe-176">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="406fe-176">Assigning users</span></span>
<span data-ttu-id="406fe-177">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="406fe-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="406fe-178">Per assegnare gli utenti a Benefitsolver, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="406fe-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="406fe-179">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="406fe-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="406fe-180">Nel * * Benefitsolver * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="406fe-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="406fe-181">![Assegnare utenti](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="406fe-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="406fe-182">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="406fe-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="406fe-183">![Sì](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="406fe-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="406fe-184">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="406fe-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="406fe-185">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="406fe-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

