---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cisco Webex | Documentazione Microsoft'
description: Informazioni su come usare Cisco Webex con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="c16a0-103">Esercitazione: Integrazione di Azure Active Directory con Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="c16a0-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="c16a0-104">Questa esercitazione descrive l'integrazione di Azure e Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="c16a0-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="c16a0-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c16a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c16a0-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="c16a0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c16a0-107">Tenant di Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="c16a0-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="c16a0-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Cisco Webex potranno accedere all'applicazione tramite il sito aziendale di Cisco Webex (accesso avviato dal provider di servizi) o seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c16a0-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c16a0-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="c16a0-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="c16a0-110">Abilitazione dell'integrazione dell'applicazione per Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="c16a0-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="c16a0-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="c16a0-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="c16a0-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="c16a0-112">Configuring user provisioning</span></span>
* <span data-ttu-id="c16a0-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="c16a0-113">Assigning users</span></span>

<span data-ttu-id="c16a0-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="c16a0-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="c16a0-115">Abilitare l'integrazione dell'applicazione per Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="c16a0-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="c16a0-116">Questa sezione descrive come abilitare l'integrazione dell'applicazione per Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="c16a0-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="c16a0-117">**Per abilitare l'integrazione dell'applicazione per Cisco Webex, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c16a0-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="c16a0-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="c16a0-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="c16a0-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c16a0-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c16a0-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="c16a0-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c16a0-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="c16a0-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="c16a0-122">![Applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="c16a0-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c16a0-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="c16a0-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="c16a0-124">![Aggiungere un'applicazione](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="c16a0-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c16a0-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="c16a0-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="c16a0-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c16a0-127">Nella **casella di ricerca** digitare **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="c16a0-128">![Raccolta di applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="c16a0-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="c16a0-129">Nel riquadro dei risultati selezionare **Cisco Webex** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c16a0-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="c16a0-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="c16a0-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c16a0-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c16a0-131">Configure single sign-on</span></span>

<span data-ttu-id="c16a0-132">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a Cisco Webex tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="c16a0-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="c16a0-133">Come parte di questa procedura, verrà richiesto di creare un file di certificato con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="c16a0-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="c16a0-134">Se non si ha familiarità con questa procedura, vedere il video che descrive [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="c16a0-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="c16a0-135">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c16a0-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c16a0-136">Nella pagina di integrazione dell'applicazione **Cisco Webex** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="c16a0-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c16a0-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="c16a0-138">Nella pagina **Stabilire come si desidera che gli utenti accedano a Cisco Webex** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="c16a0-139">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c16a0-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="c16a0-140">Nella pagina **Configura URL app** seguire questa procedura e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="c16a0-141">![Configurare l'URL dell'app](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="c16a0-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="c16a0-142">Nella casella di testo **URL di accesso** digitare l'URL del tenant di Cisco Webex, ad esempio *http://contoso.webex.com*.</span><span class="sxs-lookup"><span data-stu-id="c16a0-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="c16a0-143">Nella casella di testo **URL di risposta Cisco Webex** digitare l'**URL AssertionConsumerService di Cisco Webex**, ad esempio *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*.</span><span class="sxs-lookup"><span data-stu-id="c16a0-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="c16a0-144">Nella pagina **Configura accesso Single Sign-On in Cisco Webex** fare clic su **Scarica certificato** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="c16a0-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="c16a0-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c16a0-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="c16a0-146">In un'altra finestra del Web browser accedere al sito aziendale di Cisco Webex come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c16a0-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="c16a0-147">Nel menu in alto fare clic su **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="c16a0-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span><span class="sxs-lookup"><span data-stu-id="c16a0-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="c16a0-149">Nella sezione **Manage Site** (Gestisci sito) fare clic su **SSO Configuration** (Configurazione SSO).</span><span class="sxs-lookup"><span data-stu-id="c16a0-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="c16a0-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="c16a0-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="c16a0-151">Nella sezione Federated Web SSO Configuration seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c16a0-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="c16a0-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="c16a0-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="c16a0-153">Nell'elenco **Federation Protocol** (Protocollo federazione) selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="c16a0-154">Creare un file **con codifica Base 64** dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="c16a0-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="c16a0-155">Per informazioni dettagliate, vedere [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="c16a0-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="c16a0-156">Aprire il certificato con codifica Base 64 nel Blocco note e quindi copiarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="c16a0-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="c16a0-157">Fare clic su **Import SAML Metadata**e quindi incollare il certificato con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="c16a0-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="c16a0-158">Nella finestra di dialogo **Configura accesso Single Sign-On in Cisco Webex** del portale di Azure classico copiare il valore di **URL autorità di certificazione** e incollarlo nella casella di testo **Issuer for SAML (IdP ID)** (Autorità di certificazione per SAML - ID IdP).</span><span class="sxs-lookup"><span data-stu-id="c16a0-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="c16a0-159">Nella finestra di dialogo **Configura accesso Single Sign-On in Cisco Webex** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **Customer SSO Service Login URL** (URL di accesso al servizio clienti SSO).</span><span class="sxs-lookup"><span data-stu-id="c16a0-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="c16a0-160">Nell'elenco **NameID Format** (Formato NameID) selezionare **Email address** (Indirizzo di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="c16a0-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="c16a0-161">Nella casella di testo **AuthnContextClassRef** digitare **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="c16a0-162">Nella finestra di dialogo **Configura accesso Single Sign-On in Cisco Webex** del portale di Azure classico copiare il valore di **URL disconnessione remota** e incollarlo nella casella di testo **Customer SSO Service Logout URL** (URL di disconnessione dal servizio clienti SSO).</span><span class="sxs-lookup"><span data-stu-id="c16a0-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="c16a0-163">Fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-163">Click **Update**.</span></span>
9. <span data-ttu-id="c16a0-164">Nella finestra di dialogo **Configura accesso Single Sign-On in Cisco Webex** del portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="c16a0-165">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="c16a0-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c16a0-166">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="c16a0-166">Configure user provisioning</span></span>

<span data-ttu-id="c16a0-167">Per consentire agli utenti di Azure AD di accedere a Cisco Webex, è necessario eseguirne il provisioning in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="c16a0-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="c16a0-168">Nel caso di Cisco Webex, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="c16a0-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="c16a0-169">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c16a0-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="c16a0-170">Accedere al tenant **Cisco Webex** .</span><span class="sxs-lookup"><span data-stu-id="c16a0-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="c16a0-171">Passare a **Manage Users (Gestisci utenti) \> Add User (Aggiungi utente)**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="c16a0-172">![Aggiungere utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="c16a0-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="c16a0-173">Nella sezione Add User seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c16a0-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="c16a0-174">![Aggiungere un utente](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="c16a0-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="c16a0-175">Per **Account Type** (Tipo di account), scegliere **Host**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="c16a0-176">Digitare i dati di un utente di Azure AD esistente nelle caselle di testo seguenti: **First name, Last name** (Nome, Cognome), **User name** (Nome utente), **Email** (Indirizzo di posta elettronica), **Password**, **Confirm Password** (Conferma password).</span><span class="sxs-lookup"><span data-stu-id="c16a0-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="c16a0-177">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="c16a0-178">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Cisco Webex per eseguire il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c16a0-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="c16a0-179">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="c16a0-179">Assign users</span></span>
<span data-ttu-id="c16a0-180">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c16a0-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c16a0-181">**Per assegnare gli utenti a Cisco Webex, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="c16a0-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="c16a0-182">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="c16a0-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="c16a0-183">Nella pagina di integrazione dell'applicazione **Cisco Webex** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="c16a0-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="c16a0-184">![Assegnare utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="c16a0-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="c16a0-185">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="c16a0-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="c16a0-186">![Sì](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="c16a0-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c16a0-187">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="c16a0-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c16a0-188">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c16a0-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

