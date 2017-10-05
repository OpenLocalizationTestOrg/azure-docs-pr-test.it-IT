---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure | Documentazione Microsoft'
description: Informazioni su come usare TOPdesk - Secure con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="4e31f-103">Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="4e31f-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="4e31f-104">Questa esercitazione descrive l'integrazione di Azure e TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="4e31f-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="4e31f-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4e31f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="4e31f-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="4e31f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4e31f-107">Sottoscrizione di TOPdesk - Secure abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4e31f-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="4e31f-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a TOPdesk - Secure potranno accedere all'applicazione tramite il sito aziendale di TOPdesk - Secure (accesso avviato dal provider di servizi) o seguendo le istruzioni riportate in [Introduzione al pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e31f-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4e31f-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e31f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="4e31f-110">Abilitazione dell'integrazione dell'applicazione TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="4e31f-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="4e31f-111">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4e31f-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="4e31f-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="4e31f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="4e31f-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="4e31f-113">Assigning users</span></span>

<span data-ttu-id="4e31f-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="4e31f-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="4e31f-115">Abilitazione dell'integrazione dell'applicazione TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="4e31f-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="4e31f-116">Questa sezione descrive come abilitare l'integrazione dell'applicazione per TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="4e31f-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="4e31f-117">Per abilitare l'integrazione dell'applicazione per TOPdesk - Secure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="4e31f-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4e31f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="4e31f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4e31f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="4e31f-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="4e31f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4e31f-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="4e31f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="4e31f-122">![Applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="4e31f-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="4e31f-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="4e31f-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="4e31f-124">![Aggiungere un'applicazione](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="4e31f-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="4e31f-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="4e31f-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="4e31f-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="4e31f-127">Nella **casella di ricerca** digitare **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="4e31f-128">![Raccolta di applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="4e31f-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="4e31f-129">Nel riquadro dei risultati selezionare **TOPdesk - Secure** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4e31f-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="4e31f-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="4e31f-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="4e31f-131">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4e31f-131">Configuring single sign-on</span></span>
<span data-ttu-id="4e31f-132">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a TOPdesk - Secure tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="4e31f-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="4e31f-133">La configurazione dell'accesso Single Sign-On per TOPdesk - Secure richiede il caricamento di un file con l'icona del logo.</span><span class="sxs-lookup"><span data-stu-id="4e31f-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="4e31f-134">Per ottenere il file con l'icona, contattare il team di supporto di TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="4e31f-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="4e31f-135">Per configurare l'accesso Single Sign-On, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="4e31f-136">Accedere al sito aziendale di **TOPdesk - Secure** come un amministratore.</span><span class="sxs-lookup"><span data-stu-id="4e31f-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="4e31f-137">Nel menu **TOPdesk** fare clic su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="4e31f-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="4e31f-138">![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="4e31f-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="4e31f-139">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="4e31f-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="4e31f-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="4e31f-141">Espandere il menu **Login Settings** (Impostazioni accesso) e quindi fare clic su **General** (Generale).</span><span class="sxs-lookup"><span data-stu-id="4e31f-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="4e31f-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="4e31f-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="4e31f-143">Nell'area **Secure** (Sicura) della sezione di configurazione **SAML login** (Accesso SAML) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="4e31f-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="4e31f-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="4e31f-145">a.</span><span class="sxs-lookup"><span data-stu-id="4e31f-145">a.</span></span> <span data-ttu-id="4e31f-146">Fare clic su **Download** per scaricare il file di metadati pubblici e quindi salvarlo in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="4e31f-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="4e31f-147">b.</span><span class="sxs-lookup"><span data-stu-id="4e31f-147">b.</span></span> <span data-ttu-id="4e31f-148">Aprire il file dei metadati e quindi individuare il nodo **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="4e31f-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="4e31f-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="4e31f-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="4e31f-150">c.</span><span class="sxs-lookup"><span data-stu-id="4e31f-150">c.</span></span> <span data-ttu-id="4e31f-151">Copiare il valore di **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="4e31f-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="4e31f-152">Questo valore sarà necessario nella sezione **Configure App URL** più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4e31f-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="4e31f-153">In un'altra finestra del Web browser accedere al portale di **portale di Azure classico** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4e31f-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="4e31f-154">Nel **TOPdesk - Secure** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** per aprire il * * configurare Single Sign-On * * finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4e31f-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="4e31f-155">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4e31f-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="4e31f-156">Nella pagina **Stabilire come si desidera che gli utenti accedano a TOPdesk - Secure** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4e31f-157">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4e31f-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="4e31f-158">Nella pagina **Configura URL app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4e31f-159">![Configurare l'URL dell'app](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="4e31f-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="4e31f-160">a.</span><span class="sxs-lookup"><span data-stu-id="4e31f-160">a.</span></span> <span data-ttu-id="4e31f-161">Nella casella di testo **URL di accesso TOPdesk - Secure** digitare l'URL usato dagli utenti per accedere all'applicazione TOPdesk - Secure, ad esempio "*https://qssolutions.topdesk.net*".</span><span class="sxs-lookup"><span data-stu-id="4e31f-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="4e31f-162">b.</span><span class="sxs-lookup"><span data-stu-id="4e31f-162">b.</span></span> <span data-ttu-id="4e31f-163">Nella casella di testo **URL di risposta TOPdesk - Secure** incollare il valore dell'URL **AssertionConsumerService di TOPdesk - Secure**, ad esempio "*https://qssolutions.topdesk.net/tas/public/login/saml*"</span><span class="sxs-lookup"><span data-stu-id="4e31f-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="4e31f-164">c.</span><span class="sxs-lookup"><span data-stu-id="4e31f-164">c.</span></span> <span data-ttu-id="4e31f-165">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-165">Click **Next**.</span></span>

10. <span data-ttu-id="4e31f-166">Nella pagina **Configura accesso Single Sign-On in TOPdesk - Secure** fare clic su **Scarica metadati** per scaricare il file dei metadati e quindi salvarlo in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="4e31f-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="4e31f-167">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4e31f-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="4e31f-168">Per creare un file del certificato, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="4e31f-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="4e31f-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="4e31f-170">a.</span><span class="sxs-lookup"><span data-stu-id="4e31f-170">a.</span></span> <span data-ttu-id="4e31f-171">Aprire il file dei metadati scaricato.</span><span class="sxs-lookup"><span data-stu-id="4e31f-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="4e31f-172">b.</span><span class="sxs-lookup"><span data-stu-id="4e31f-172">b.</span></span> <span data-ttu-id="4e31f-173">Espandere il nodo **RoleDescriptor** con **xsi:type** corrispondente a **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="4e31f-174">c.</span><span class="sxs-lookup"><span data-stu-id="4e31f-174">c.</span></span> <span data-ttu-id="4e31f-175">Copiare il valore del nodo **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="4e31f-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="4e31f-176">d.</span><span class="sxs-lookup"><span data-stu-id="4e31f-176">d.</span></span> <span data-ttu-id="4e31f-177">Salvare il valore copiato di **X509Certificate** in un file locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="4e31f-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="4e31f-178">Nel sito aziendale di TOPdesk - Secure scegliere **Settings** (Impostazioni) dal menu **TOPdesk**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="4e31f-179">![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="4e31f-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="4e31f-180">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="4e31f-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="4e31f-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="4e31f-182">Espandere il menu **Login Settings** (Impostazioni accesso) e quindi fare clic su **General** (Generale).</span><span class="sxs-lookup"><span data-stu-id="4e31f-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="4e31f-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="4e31f-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="4e31f-184">Nell'area **Public** (Pubblica) fare clic su **Add** (Aggiungi).</span><span class="sxs-lookup"><span data-stu-id="4e31f-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="4e31f-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span><span class="sxs-lookup"><span data-stu-id="4e31f-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="4e31f-186">Nella pagina **SAML configuration assistant** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="4e31f-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="4e31f-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="4e31f-188">a.</span><span class="sxs-lookup"><span data-stu-id="4e31f-188">a.</span></span> <span data-ttu-id="4e31f-189">Per caricare il file di metadati scaricato, in **Federation Metadata** (Metadati configurazione) fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="4e31f-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="4e31f-190">b.</span><span class="sxs-lookup"><span data-stu-id="4e31f-190">b.</span></span> <span data-ttu-id="4e31f-191">Per caricare il file del certificato, in **Certificate (RSA)** (Certificato RSA) fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="4e31f-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="4e31f-192">c.</span><span class="sxs-lookup"><span data-stu-id="4e31f-192">c.</span></span> <span data-ttu-id="4e31f-193">Per caricare il file del logo ottenuto dal team di supporto del team di TOPdesk, in **Logo icon** (Icona logo) fare clic su **Browse** (Sfoglia).</span><span class="sxs-lookup"><span data-stu-id="4e31f-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="4e31f-194">d.</span><span class="sxs-lookup"><span data-stu-id="4e31f-194">d.</span></span> <span data-ttu-id="4e31f-195">Nella casella di testo **User name attribute** (Attributo nome utente) digitare **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="4e31f-196">e.</span><span class="sxs-lookup"><span data-stu-id="4e31f-196">e.</span></span> <span data-ttu-id="4e31f-197">Nella casella di testo **Display name** digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="4e31f-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="4e31f-198">f.</span><span class="sxs-lookup"><span data-stu-id="4e31f-198">f.</span></span> <span data-ttu-id="4e31f-199">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-199">Click **Save**.</span></span>

17. <span data-ttu-id="4e31f-200">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="4e31f-201">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4e31f-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="4e31f-202">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="4e31f-202">Configuring user provisioning</span></span>
<span data-ttu-id="4e31f-203">Per consentire agli utenti di Azure AD di accedere a TOPdesk - Secure, è necessario eseguirne il provisioning in TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="4e31f-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="4e31f-204">Nel caso di TOPdesk - Secure, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4e31f-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4e31f-205">Per configurare il provisioning utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="4e31f-206">Accedere al sito aziendale di **TOPdesk - Secure** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4e31f-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="4e31f-207">Nel menu in alto fare clic su **TOPdesk \> New (Nuovo) \> Support Files (File di supporto) \> Operator (Operatore)**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="4e31f-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="4e31f-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="4e31f-209">Nella finestra di dialogo **New Operator** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4e31f-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span><span class="sxs-lookup"><span data-stu-id="4e31f-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="4e31f-211">a.</span><span class="sxs-lookup"><span data-stu-id="4e31f-211">a.</span></span> <span data-ttu-id="4e31f-212">Fare clic sulla scheda General.</span><span class="sxs-lookup"><span data-stu-id="4e31f-212">Click the General tab.</span></span>
   
    <span data-ttu-id="4e31f-213">b.</span><span class="sxs-lookup"><span data-stu-id="4e31f-213">b.</span></span> <span data-ttu-id="4e31f-214">Nella casella di testo **Surname** (Cognome) della sezione **General** (Generale) digitare il cognome di un account di Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="4e31f-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="4e31f-215">c.</span><span class="sxs-lookup"><span data-stu-id="4e31f-215">c.</span></span> <span data-ttu-id="4e31f-216">Nella sezione **Location** (Località) selezionare un sito dalla casella **Site** (Sito).</span><span class="sxs-lookup"><span data-stu-id="4e31f-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="4e31f-217">d.</span><span class="sxs-lookup"><span data-stu-id="4e31f-217">d.</span></span> <span data-ttu-id="4e31f-218">Nella casella di testo **Login Name** (Nome di accesso) della sezione **TOPdesk Login** (Accesso TOPdesk) digitare un nome di accesso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="4e31f-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="4e31f-219">e.</span><span class="sxs-lookup"><span data-stu-id="4e31f-219">e.</span></span> <span data-ttu-id="4e31f-220">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4e31f-221">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da TOPdesk - Secure per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e31f-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="4e31f-222">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="4e31f-222">Assigning users</span></span>
<span data-ttu-id="4e31f-223">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4e31f-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="4e31f-224">Per assegnare gli utenti a TOPdesk - Secure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4e31f-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="4e31f-225">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="4e31f-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4e31f-226">Nel * * TOPdesk - Secure * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4e31f-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="4e31f-227">![Assegnare utenti](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="4e31f-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="4e31f-228">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="4e31f-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="4e31f-229">![Sì](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="4e31f-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4e31f-230">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4e31f-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="4e31f-231">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4e31f-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

