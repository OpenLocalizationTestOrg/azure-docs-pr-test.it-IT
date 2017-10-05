---
title: 'Esercitazione: Integrazione di Azure Active Directory con Central Desktop | Documentazione Microsoft'
description: Informazioni su come usare Central Desktop con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="1e23e-103">Esercitazione: Integrazione di Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e23e-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="1e23e-104">Questa esercitazione descrive l'integrazione di Azure e Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="1e23e-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1e23e-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="1e23e-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="1e23e-106">A valid Azure subscription</span></span>
* <span data-ttu-id="1e23e-107">Sottoscrizione di Central Desktop abilitata per l'accesso Single Sign-On e tenant di Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e23e-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="1e23e-108">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e23e-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="1e23e-109">Abilitazione dell'integrazione dell'applicazione per Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e23e-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="1e23e-110">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="1e23e-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="1e23e-111">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="1e23e-111">Configuring user provisioning</span></span>
* <span data-ttu-id="1e23e-112">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="1e23e-112">Assigning users</span></span>

<span data-ttu-id="1e23e-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="1e23e-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="1e23e-114">Abilitare l'integrazione dell'applicazione per Central Desktop</span><span class="sxs-lookup"><span data-stu-id="1e23e-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="1e23e-115">Questa sezione descrive come abilitare l'integrazione dell'applicazione per Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="1e23e-116">**Per abilitare l'integrazione dell'applicazione per Central Desktop, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1e23e-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1e23e-117">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="1e23e-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="1e23e-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1e23e-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="1e23e-119">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="1e23e-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1e23e-120">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="1e23e-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="1e23e-121">![Applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="1e23e-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="1e23e-122">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="1e23e-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="1e23e-123">![Aggiungere un'applicazione](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="1e23e-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="1e23e-124">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="1e23e-125">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="1e23e-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="1e23e-126">Nella **casella di ricerca** digitare **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="1e23e-127">![Raccolta di applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="1e23e-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="1e23e-128">Nel riquadro dei risultati selezionare **Central Desktop** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e23e-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="1e23e-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="1e23e-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="1e23e-130">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1e23e-130">Configure single sign-on</span></span>

<span data-ttu-id="1e23e-131">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a Central Desktop tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="1e23e-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="1e23e-132">Come parte di questa procedura, verrà richiesto di caricare un file di certificato con codifica Base 64 nel tenant di Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="1e23e-133">Se non si ha familiarità con questa procedura, vedere il video che illustra [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="1e23e-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="1e23e-134">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1e23e-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="1e23e-135">Nel portale di Azure classico, nel **Central Desktop** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** per aprire il * * configurare Single Sign-On * * finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1e23e-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="1e23e-136">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e23e-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="1e23e-137">Nella pagina **Stabilire come si desidera che gli utenti accedano a Central Desktop** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="1e23e-138">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e23e-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="1e23e-139">Nella pagina **Configura URL app** seguire questa procedura e quindi fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="1e23e-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="1e23e-140">Nella casella di testo **URL accesso Central Desktop** digitare l'URL del tenant di Central Desktop, ad esempio *http://contoso.centraldesktop.com*.</span><span class="sxs-lookup"><span data-stu-id="1e23e-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="1e23e-141">Nella casella di testo URL di risposta Central Desktop digitare l'URL AssertionConsumerService di Central Desktop, ad esempio https://contoso.centraldesktop.com/saml2-assertion.php.</span><span class="sxs-lookup"><span data-stu-id="1e23e-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1e23e-142">È possibile ottenere il valore dai metadati di Central Desktop, ad esempio *http://contoso.centraldesktop.com*.</span><span class="sxs-lookup"><span data-stu-id="1e23e-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="1e23e-143">![Configurare l'URL dell'app](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="1e23e-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="1e23e-144">Nella pagina **Configura accesso Single Sign-On in Central Desktop** fare clic su **Scarica certificato** per scaricare il file di certificato e quindi salvarlo nel computer.</span><span class="sxs-lookup"><span data-stu-id="1e23e-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="1e23e-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e23e-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="1e23e-146">Accedere al tenant di **Central Desktop** .</span><span class="sxs-lookup"><span data-stu-id="1e23e-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="1e23e-147">Passare a **Settings** (Impostazioni), fare clic su **Advanced** (Avanzate) e quindi su **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="1e23e-148">![Installazione - Avanzate](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Installazione - Avanzate")</span><span class="sxs-lookup"><span data-stu-id="1e23e-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="1e23e-149">Nella pagina **Single Sign-On Settings** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e23e-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="1e23e-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="1e23e-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="1e23e-151">Selezionare **Enable SAML v2 Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="1e23e-152">Nella pagina **Configura accesso Single Sign-On in Central Desktop** del portale di Azure classico copiare il valore di **URL autorità di certificazione** e incollarlo nella casella di testo **URL SSO**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="1e23e-153">Nella pagina **Configura accesso Single Sign-On in Central Desktop** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **SSO Login URL** (URL di accesso SSO).</span><span class="sxs-lookup"><span data-stu-id="1e23e-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="1e23e-154">Nella pagina **Configura accesso Single Sign-On in Central Desktop** del portale di Azure classico copiare il valore di **URL servizio Single Sign-Out** e incollarlo nella casella di testo **SSO Logout URL** (URL disconnessione SSO).</span><span class="sxs-lookup"><span data-stu-id="1e23e-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="1e23e-155">Nella sezione **Message Signature Verification Method** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e23e-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="1e23e-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span><span class="sxs-lookup"><span data-stu-id="1e23e-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="1e23e-157">Selezionare **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="1e23e-158">Nell'elenco **SSO Certificate** (Certificato SSO) selezionare **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="1e23e-159">Creare un file di testo dal certificato scaricato, copiare il contenuto del file di testo e quindi incollarlo nel campo **SSO Certificate** .</span><span class="sxs-lookup"><span data-stu-id="1e23e-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="1e23e-160">Per informazioni dettagliate, vedere [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="1e23e-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="1e23e-161">Selezionare **Display a link to your SAMLv2 login page**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="1e23e-162">Fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-162">Click **Update**.</span></span>
10. <span data-ttu-id="1e23e-163">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="1e23e-164">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="1e23e-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="1e23e-165">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="1e23e-165">Configure user provisioning</span></span>

<span data-ttu-id="1e23e-166">Per consentire agli utenti di AAD di accedere, è necessario eseguirne il provisioning nell'applicazione Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="1e23e-167">Questa sezione descrive come creare account utente di AAD in Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="1e23e-168">**Per eseguire il provisioning degli account utente in Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="1e23e-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="1e23e-169">Accedere al tenant di Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="1e23e-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="1e23e-170">Passare a **People \> Internal Members** (Persone > Membri interni).</span><span class="sxs-lookup"><span data-stu-id="1e23e-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="1e23e-171">Fare clic su **Add Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="1e23e-172">![Persone](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="1e23e-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="1e23e-173">Nella casella di testo **Email Address of New Members** (Indirizzo posta elettronica nuovi membri) digitare un account AAD di cui si vuole eseguire il provisioning e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="1e23e-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="1e23e-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span><span class="sxs-lookup"><span data-stu-id="1e23e-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="1e23e-175">Fare clic su **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="1e23e-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span><span class="sxs-lookup"><span data-stu-id="1e23e-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1e23e-177">Gli utenti aggiunti riceveranno un messaggio di posta elettronica che include un collegamento di conferma su cui dovranno fare clic per attivare l'account.</span><span class="sxs-lookup"><span data-stu-id="1e23e-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="1e23e-178">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Central Desktop per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e23e-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="1e23e-179">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="1e23e-179">Assign users</span></span>
<span data-ttu-id="1e23e-180">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e23e-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="1e23e-181">**Per assegnare gli utenti a Central Desktop, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="1e23e-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="1e23e-182">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="1e23e-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="1e23e-183">Nella pagina di integrazione dell'applicazione **Central Desktop** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e23e-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="1e23e-184">![Assegnare utenti](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="1e23e-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="1e23e-185">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="1e23e-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="1e23e-186">![Sì](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="1e23e-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="1e23e-187">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e23e-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1e23e-188">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e23e-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

