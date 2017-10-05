---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs'
description: Informazioni su come usare SAP HANA Cloud Platform con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="e5649-103">Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="e5649-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="e5649-104">In questa esercitazione viene illustrata l'integrazione di Azure e SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="e5649-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e5649-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="e5649-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="e5649-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e5649-107">Account di SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="e5649-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="e5649-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a SAP HANA Cloud Platform saranno in grado di eseguire l'accesso Single Sign-On all'applicazione seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5649-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="e5649-109">È necessario distribuire l'applicazione o la sottoscrizione a un'applicazione per l'account di SAP HANA Cloud Platform per testare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e5649-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="e5649-110">In questa esercitazione, viene distribuita un'applicazione nell'account.</span><span class="sxs-lookup"><span data-stu-id="e5649-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="e5649-111">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e5649-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="e5649-112">Abilitazione dell'integrazione dell'applicazione per SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="e5649-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="e5649-113">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="e5649-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e5649-114">Assegnazione di un ruolo a un utente</span><span class="sxs-lookup"><span data-stu-id="e5649-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="e5649-115">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="e5649-115">Assigning users</span></span>

<span data-ttu-id="e5649-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="e5649-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="e5649-117">Abilitazione dell'integrazione dell'applicazione per SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="e5649-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="e5649-118">In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="e5649-119">**Per abilitare l'integrazione dell'applicazione per SAP HANA Cloud Platform, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e5649-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="e5649-120">Nel portale di gestione di Azure fare clic su **Active Directory**nel pannello di navigazione sinistro.</span><span class="sxs-lookup"><span data-stu-id="e5649-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="e5649-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e5649-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e5649-122">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="e5649-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e5649-123">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="e5649-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="e5649-124">![Applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="e5649-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e5649-125">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="e5649-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="e5649-126">![Aggiungere un'applicazione](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="e5649-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e5649-127">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="e5649-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="e5649-128">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="e5649-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e5649-129">Nella **casella di ricerca** digitare **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="e5649-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="e5649-130">![Raccolta di applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="e5649-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="e5649-131">Nel riquadro dei risultati selezionare **SAP HANA Cloud Platform**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5649-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="e5649-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="e5649-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e5649-133">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e5649-133">Configure single sign-on</span></span>

<span data-ttu-id="e5649-134">In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a SAP HANA Cloud Platform tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="e5649-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="e5649-135">Per eseguire questa procedura, è necessario caricare un file di certificato con codifica Base 64 nel proprio tenant SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="e5649-136">Se non si ha familiarità con questa procedura, vedere il video che descrive [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="e5649-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="e5649-137">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e5649-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="e5649-138">Nella pagina di integrazione dell'applicazione **SAP HANA Cloud Platform** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="e5649-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="e5649-139">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e5649-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="e5649-140">Nella pagina **Stabilire come si desidera che gli utenti accedano a SAP HANA Cloud Platform** selezionare **Single Sign-On di Microsoft Azure AD**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e5649-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="e5649-141">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e5649-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="e5649-142">In una diversa finestra del Web browser accedere al pannello di controllo di SAP HANA Cloud Platform in https://account.\<landscape host\>.ondemand.com/cockpit (ad esempio *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="e5649-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="e5649-143">Scegliere la scheda **Trust** .</span><span class="sxs-lookup"><span data-stu-id="e5649-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="e5649-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="e5649-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="e5649-145">Nella sezione relativa alla gestione dell'attendibilità, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e5649-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="e5649-146">![Ottenere i metadati](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Ottenere i metadati")</span><span class="sxs-lookup"><span data-stu-id="e5649-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="e5649-147">Fare clic sulla scheda **Local Service Provider** .</span><span class="sxs-lookup"><span data-stu-id="e5649-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="e5649-148">Per scaricare il file di metadati di SAP HANA Cloud Platform, fare clic su **Get Metadata**.</span><span class="sxs-lookup"><span data-stu-id="e5649-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="e5649-149">Nella pagina **Configura URL app** del portale di Azure Active classico eseguire la procedura seguente e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="e5649-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="e5649-150">![Configurare l'URL dell'app](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="e5649-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="e5649-151">Nella casella di testo **URL di accesso** digitare l'URL utilizzato dagli utenti per accedere all'applicazione **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="e5649-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="e5649-152">Questo è l'URL specifico dell'account di una risorsa protetta dell'applicazione SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="e5649-153">L'URL è basato sul modello seguente: *https://\<nomeApplicazione\>\<nomeAccount\>.\<landscape host\>.ondemand.com/\<percorso\_alle\_risosrse\_protette\>* (ad esempio *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="e5649-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="e5649-154">Questo è l'URL dell'applicazione SAP HANA Cloud Platform che richiede l’autenticazione dell’utente.</span><span class="sxs-lookup"><span data-stu-id="e5649-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="e5649-155">Aprire il file di metadati SAP HANA Cloud piattaforma scaricato e quindi individuare il tag **ns3:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="e5649-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="e5649-156">Copiare il valore dell'attributo **Percorso** e incollarlo nella casella di testo **SAP HANA Cloud Platform Reply URL**.</span><span class="sxs-lookup"><span data-stu-id="e5649-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="e5649-157">Nella pagina **Configura accesso Single Sign-On in SAP HANA Cloud Platform** fare clic su **Scarica metadati** per scaricare i metadati e salvare il file nel computer.</span><span class="sxs-lookup"><span data-stu-id="e5649-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="e5649-158">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e5649-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="e5649-159">Nel pannello di controllo di SAP HANA Cloud Platform, nella sezione **Local Service Provider** , eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e5649-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e5649-160">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="e5649-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="e5649-161">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="e5649-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="e5649-162">In **Configuration Type** selezionare **Custom**.</span><span class="sxs-lookup"><span data-stu-id="e5649-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="e5649-163">In **Local Provider Name**lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="e5649-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="e5649-164">Per generare una **chiave per la firma** e una coppia di chiavi del **certificato di firma**, fare clic su **Generate Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="e5649-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="e5649-165">In **Propagazione entità** selezionare **Disabilitato**.</span><span class="sxs-lookup"><span data-stu-id="e5649-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="e5649-166">In **Force Authentication** selezionare **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="e5649-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="e5649-167">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5649-167">Click **Save**.</span></span>

9. <span data-ttu-id="e5649-168">Fare clic sulla scheda **Trusted Identity Provider**, quindi fare clic su **Add Trusted Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="e5649-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="e5649-169">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="e5649-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e5649-170">Per gestire l'elenco dei provider di identità attendibili, è necessario aver scelto il tipo di configurazione Personalizza nella sezione Provider di servizi locale.</span><span class="sxs-lookup"><span data-stu-id="e5649-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="e5649-171">Per il tipo di configurazione predefinito è presente una relazione di trust implicita e non modificabile per il servizio SAP ID.</span><span class="sxs-lookup"><span data-stu-id="e5649-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="e5649-172">Per Nessuno, non sono disponibili impostazioni di trust.</span><span class="sxs-lookup"><span data-stu-id="e5649-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="e5649-173">Fare clic sulla scheda **General**, quindi fare clic su **Browse** per caricare il file di metadati scaricati.</span><span class="sxs-lookup"><span data-stu-id="e5649-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="e5649-174">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="e5649-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="e5649-175">Dopo aver caricato il file di metadati, i valori per **URL Single Sign-On**, **URL disconnessione singola** e **Certificato di firma** vengono popolati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e5649-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="e5649-176">Fare clic sulla scheda **Attributes** .</span><span class="sxs-lookup"><span data-stu-id="e5649-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="e5649-177">Nella scheda **Attributes** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e5649-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="e5649-178">![Attributi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="e5649-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="e5649-179">Fare clic su **Add Assertion-Based Attribute** e quindi aggiungere gli attributi basati su asserzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="e5649-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="e5649-180">Attributo di asserzione</span><span class="sxs-lookup"><span data-stu-id="e5649-180">Assertion Attribute</span></span> | <span data-ttu-id="e5649-181">Attributo di entità</span><span class="sxs-lookup"><span data-stu-id="e5649-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="e5649-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="e5649-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="e5649-183">firstname</span><span class="sxs-lookup"><span data-stu-id="e5649-183">firstname</span></span> |
    | <span data-ttu-id="e5649-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="e5649-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="e5649-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="e5649-185">lastname</span></span> |
    | <span data-ttu-id="e5649-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="e5649-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="e5649-187">email</span><span class="sxs-lookup"><span data-stu-id="e5649-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="e5649-188">La configurazione degli attributi dipende da come le applicazioni per HPC vengono sviluppate, vale a dire quali attributi sono previsti nella risposta SAML e con quale nome (attributo di entità) accedono a questo attributo nel codice.</span><span class="sxs-lookup"><span data-stu-id="e5649-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="e5649-189">L'**attributo predefinito** presente nella schermata è solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="e5649-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="e5649-190">Non è necessario per il funzionamento dello scenario.</span><span class="sxs-lookup"><span data-stu-id="e5649-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="e5649-191">I nomi e i valori per l'**attributo di entità** illustrati nella schermata dipendono dal modo in cui viene sviluppata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5649-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="e5649-192">È possibile che l'applicazione richieda mapping diversi.</span><span class="sxs-lookup"><span data-stu-id="e5649-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="e5649-193">Nella pagina della finestra di dialogo **Configure single sign-on at SAP HANA Cloud Platform** (Configura accesso Single Sign-On in SAP HANA Cloud Platform) del portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On, quindi fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="e5649-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="e5649-194">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="e5649-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="e5649-195">Gruppi basati su asserzione</span><span class="sxs-lookup"><span data-stu-id="e5649-195">Assertion-based groups</span></span>
<span data-ttu-id="e5649-196">Come passaggio facoltativo, è possibile configurare gruppi basati su asserzione per il provider di identità Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5649-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="e5649-197">L'uso dei gruppi in SAP HANA Cloud Platform consente di assegnare dinamicamente uno o più utenti a uno o più ruoli nelle applicazioni SAP HANA Cloud Platform, determinate dai valori degli attributi nell'asserzione SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="e5649-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="e5649-198">Ad esempio, se l'asserzione contiene l'attributo "*contract=temporary*", si potrebbe volere che tutti gli utenti interessati siano aggiunti al gruppo"*TEMPORARY*".</span><span class="sxs-lookup"><span data-stu-id="e5649-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="e5649-199">Il gruppo "*TEMPORARY*" può contenere uno o più ruoli da uno o più applicazioni distribuite nell'account di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="e5649-200">Usare i gruppi basati su asserzione quando si vogliono assegnare simultaneamente diversi utenti a uno o più ruoli delle applicazioni nell'account di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="e5649-201">Per assegnare un singolo utente o un numero ridotto di utenti a ruoli specifici, è consigliabile di eseguirne l'assegnazione diretta nella scheda **Authorizations** (Autorizzazioni) del pannello di controllo di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="e5649-202">Assegnare un ruolo a un utente</span><span class="sxs-lookup"><span data-stu-id="e5649-202">Assign a role to a user</span></span>
<span data-ttu-id="e5649-203">Per consentire agli utenti di Azure AD di accedere a SAP HANA Cloud Platform è necessario assegnare loro i ruoli in SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="e5649-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="e5649-204">**Per assegnare un ruolo a un utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e5649-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="e5649-205">Accedere al pannello di controllo di **SAP HANA Cloud Platform** .</span><span class="sxs-lookup"><span data-stu-id="e5649-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="e5649-206">Eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="e5649-206">Perform the following:</span></span>
   
   <span data-ttu-id="e5649-207">![Autorizzazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizzazioni")</span><span class="sxs-lookup"><span data-stu-id="e5649-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="e5649-208">Fare clic su **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="e5649-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="e5649-209">Fare clic sulla scheda **Users** .</span><span class="sxs-lookup"><span data-stu-id="e5649-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="e5649-210">Nella casella di testo **User** digitare l'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e5649-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="e5649-211">Fare clic su **Assign** per assegnare l'utente a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="e5649-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="e5649-212">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5649-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="e5649-213">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="e5649-213">Assign users</span></span>
<span data-ttu-id="e5649-214">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5649-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="e5649-215">**Per assegnare gli utenti a SAP HANA Cloud Platform, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="e5649-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="e5649-216">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="e5649-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e5649-217">Nella pagina di integrazione di **SAP HANA Cloud Platform** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="e5649-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e5649-218">![Assegnare utenti](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="e5649-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="e5649-219">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="e5649-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="e5649-220">![Sì](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="e5649-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e5649-221">Per testare le impostazioni di SSO, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e5649-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="e5649-222">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5649-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

