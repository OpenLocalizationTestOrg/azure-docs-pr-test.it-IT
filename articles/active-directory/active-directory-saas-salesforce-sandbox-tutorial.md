---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Documentazione Microsoft'
description: Informazioni su come usare Salesforce Sandbox con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="0dcda-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0dcda-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="0dcda-104">In questa esercitazione viene illustrata l'integrazione di Azure e Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0dcda-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="0dcda-105">Per commenti, vedere la [pagina del supporto tecnico Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="0dcda-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="0dcda-106">Sandbox offre la possibilità di creare più copie dell'organizzazione in ambienti distinti per diversi scopi, ad esempio sviluppo, test e formazione, senza compromettere i dati e le applicazioni dell’organizzazione di produzione Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0dcda-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="0dcda-107">Per ulteriori informazioni, vedere [Panoramica di Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="0dcda-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="0dcda-108">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0dcda-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="0dcda-109">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="0dcda-109">A valid Azure subscription</span></span>
* <span data-ttu-id="0dcda-110">Sandbox in Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="0dcda-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="0dcda-111">Se non si dispone di un sandbox valido in Salesforce.com, è necessario contattare Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0dcda-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="0dcda-112">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dcda-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="0dcda-113">Abilitazione dell'integrazione dell'applicazione per Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0dcda-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="0dcda-114">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="0dcda-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="0dcda-115">Abilitazione del dominio</span><span class="sxs-lookup"><span data-stu-id="0dcda-115">Enabling your domain</span></span>
4. <span data-ttu-id="0dcda-116">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="0dcda-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="0dcda-117">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="0dcda-117">Assigning users</span></span>

<span data-ttu-id="0dcda-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="0dcda-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="0dcda-119">Abilitare l'integrazione dell'applicazione per Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="0dcda-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="0dcda-120">In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0dcda-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="0dcda-121">**Per abilitare l'integrazione dell'applicazione per Salesforce Sandbox, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0dcda-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="0dcda-122">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="0dcda-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="0dcda-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="0dcda-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="0dcda-124">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="0dcda-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="0dcda-125">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="0dcda-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="0dcda-126">![Applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="0dcda-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="0dcda-127">Per aprire la **Raccolta di applicazioni**, fare clic su **Aggiungi app**, quindi fare clic su **Aggiungi un'applicazione che verrà utilizzata dall'organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="0dcda-128">![Come procedere](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Come procedere")</span><span class="sxs-lookup"><span data-stu-id="0dcda-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="0dcda-129">Nella **casella di ricerca** digitare **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="0dcda-130">![Raccolta di applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="0dcda-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="0dcda-131">Nel riquadro dei risultati selezionare **Salesforce Sandbox**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dcda-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="0dcda-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="0dcda-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="0dcda-133">Configurare l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="0dcda-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="0dcda-134">In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a Salesforce Sandbox tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="0dcda-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="0dcda-135">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0dcda-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="0dcda-136">Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="0dcda-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0dcda-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="0dcda-138">Nella pagina **Stabilire come si desidera che gli utenti accedano a Salesforce Sandbox** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="0dcda-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="0dcda-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="0dcda-140">Nella casella di testo **URL di accesso** della pagina **Configura URL app** digitare l'URL nel formato `http://company.my.salesforce.com` e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="0dcda-141">![Configurare l'URL dell'app](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="0dcda-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="0dcda-142">Se l'accesso Single Sign-On è già stato configurato per un'altra istanza di Salesforce Sandbox nella directory, sarà necessario configurare anche l'**identificatore** in modo che abbia lo stesso valore di **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="0dcda-143">Per trovare il campo **Identificatore**, selezionare la casella di controllo **Impostazioni avanzate** nella pagina **Configura URL app** della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0dcda-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="0dcda-144">Nella pagina **Configura accesso Single Sign-On in Salesforce Sandbox** fare clic su **Scarica certificato** e quindi salvare il file di certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="0dcda-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="0dcda-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0dcda-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="0dcda-146">In un'altra finestra del Web browser accedere al sito aziendale di Salesforce Sandbox come amministratore.</span><span class="sxs-lookup"><span data-stu-id="0dcda-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="0dcda-147">Nel menu in alto fare clic su **Impostazione**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="0dcda-148">![Installazione](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="0dcda-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="0dcda-149">Nel riquadro di spostamento a sinistra, fare clic su **Security Controls** (Controlli di sicurezza) e quindi fare clic su **Single Sign-On Settings** (Impostazioni Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="0dcda-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="0dcda-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="0dcda-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="0dcda-151">Nella sezione Impostazioni Single Sign-On, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0dcda-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="0dcda-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="0dcda-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="0dcda-153">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="0dcda-154">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-154">Click **New**.</span></span>
10. <span data-ttu-id="0dcda-155">Nella sezione Impostazioni SAML Single Sign-On, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0dcda-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="0dcda-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="0dcda-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="0dcda-157">Nella casella di testo Nome digitare il nome della configurazione, ad esempio *SPSSOWAAD\_Test*.</span><span class="sxs-lookup"><span data-stu-id="0dcda-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="0dcda-158">Nella finestra di dialogo **Configura accesso Single Sign-On in Salesforce Sandbox** del portale di Azure classico copiare il valore di **URL autorità di certificazione** e incollarlo nella casella di testo **Issuer** (Autorità di certificazione).</span><span class="sxs-lookup"><span data-stu-id="0dcda-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="0dcda-159">Nella casella di testo **ID entità** digitare **https://test.salesforce.com** se è la prima istanza di Salesforce Sandbox aggiunta alla directory.</span><span class="sxs-lookup"><span data-stu-id="0dcda-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="0dcda-160">Se esiste già un'istanza di Salesforce Sandbox, in **ID entità** digitare l'**URL di accesso**, che deve avere questo formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0dcda-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="0dcda-161">Per caricare il certificato scaricato, fare clic su **Sfoglia** .</span><span class="sxs-lookup"><span data-stu-id="0dcda-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="0dcda-162">In **SAML Identity Type** (Tipo di identità SAML) selezionare **Assertion contains the Federation ID from the User object** (L'asserzione contiene l'ID federazione dell'oggetto utente).</span><span class="sxs-lookup"><span data-stu-id="0dcda-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="0dcda-163">In **SAML Identity Location**(Percorso identità SAML) selezionare **Identity is in the NameIdentifier element of the Subject statement** (L'identità è nell'elemento NameIdentifier dell'istruzione Subject).</span><span class="sxs-lookup"><span data-stu-id="0dcda-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="0dcda-164">Nella pagina della finestra di dialogo **Configura accesso Single Sign-On in Salesforce Sandbox** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **Identity Provider Login URL** (URL di accesso provider di identità).</span><span class="sxs-lookup"><span data-stu-id="0dcda-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="0dcda-165">SFDC non supporta la disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="0dcda-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="0dcda-166">Come soluzione alternativa, incollare "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" nella casella di testo **Identity Provider Logout URL** (URL di disconnessione provider di identità).</span><span class="sxs-lookup"><span data-stu-id="0dcda-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="0dcda-167">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="0dcda-168">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-168">Click **Save**.</span></span>
11. <span data-ttu-id="0dcda-169">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="0dcda-170">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0dcda-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="0dcda-171">Abilitare il dominio</span><span class="sxs-lookup"><span data-stu-id="0dcda-171">Enable your domain</span></span>
<span data-ttu-id="0dcda-172">In questa sezione si presuppone che sia già stato creato un dominio.</span><span class="sxs-lookup"><span data-stu-id="0dcda-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="0dcda-173">Per informazioni dettagliate, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="0dcda-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="0dcda-174">**Per abilitare il dominio, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0dcda-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="0dcda-175">Nel riquadro di spostamento a sinistra fare clic su **Domain Management** (Gestione dominio) e quindi su **My Domain** (Dominio personale).</span><span class="sxs-lookup"><span data-stu-id="0dcda-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="0dcda-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="0dcda-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="0dcda-177">Assicurarsi che il dominio sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="0dcda-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="0dcda-178">Nella sezione **Login Page Settings** (Impostazioni pagina di accesso) fare clic su **Edit** (Modifica), quindi per **Authentication Service** (Servizio di autenticazione) selezionare il nome dell'impostazione Single Sign-On SAML definita nella sezione precedente e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="0dcda-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="0dcda-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="0dcda-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="0dcda-180">Non appena si dispone di un dominio configurato, gli utenti devono utilizzare l'URL del dominio per l'accesso a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0dcda-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="0dcda-181">Per ottenere il valore dell'URL, fare clic sul profilo SSO creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="0dcda-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="0dcda-182">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="0dcda-182">Configure user provisioning</span></span>
<span data-ttu-id="0dcda-183">In questa sezione viene descritto come abilitare il provisioning utente degli account utente di Active Directory in Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0dcda-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="0dcda-184">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="0dcda-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0dcda-185">Nella barra di spostamento in alto del portale di Salesforce, selezionare il nome per espandere il menu utente:</span><span class="sxs-lookup"><span data-stu-id="0dcda-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="0dcda-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="0dcda-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="0dcda-187">Nel menu utente selezionare **My Settings** (Impostazioni personali) per aprire la pagina **My Settings** (Impostazioni personali).</span><span class="sxs-lookup"><span data-stu-id="0dcda-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="0dcda-188">Nel riquadro a sinistra fare clic su **Personal** (Personale) per espandere la sezione corrispondente e fare clic su **Reset My Security Token** (Reimposta token di sicurezza personale):</span><span class="sxs-lookup"><span data-stu-id="0dcda-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="0dcda-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="0dcda-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="0dcda-190">Nella pagina **Reset My Security Token** (Reimposta token di sicurezza personale) fare clic su **Reset Security Token** (Reimposta token di sicurezza) per richiedere un messaggio di posta elettronica con il token di sicurezza di Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="0dcda-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="0dcda-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span><span class="sxs-lookup"><span data-stu-id="0dcda-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="0dcda-192">Verificare nella cartella Posta in arrivo la presenza di un messaggio da Salesforce.com con oggetto analogo a "**conferma di sicurezza di salesforce.com.com**".</span><span class="sxs-lookup"><span data-stu-id="0dcda-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="0dcda-193">Aprire il messaggio di posta elettronica e copiare il valore del token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0dcda-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="0dcda-194">Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** del portale di Azure classico fare clic su **Configura provisioning utenti** per aprire la finestra di dialogo **Configura provisioning utenti**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="0dcda-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span><span class="sxs-lookup"><span data-stu-id="0dcda-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="0dcda-196">Nella pagina **Immettere le credenziali di Salesforce Sandbox per abilitare il provisioning automatico degli utenti** specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="0dcda-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="0dcda-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="0dcda-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="0dcda-198">Nella casella di testo **Nome utente amministratore Salesforce Sandbox** digitare un nome account di Salesforce Sandbox con il profilo **Amministratore di sistema** assegnato in Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="0dcda-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="0dcda-199">Nella casella di testo **Password amministratore Salesforce Sandbox** digitare la password per questo account.</span><span class="sxs-lookup"><span data-stu-id="0dcda-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="0dcda-200">Nella casella di testo **Token di sicurezza utente** incollare il valore del token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0dcda-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="0dcda-201">Fare clic su **Convalida** per verificare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="0dcda-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="0dcda-202">Fare clic sul pulsante **Avanti** per aprire la pagina **Conferma**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="0dcda-203">Nella pagina **Conferma** fare clic su **Completa** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="0dcda-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="0dcda-204">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="0dcda-204">Assigning users</span></span>

<span data-ttu-id="0dcda-205">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0dcda-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="0dcda-206">**Per assegnare gli utenti a Salesforce Sandbox, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0dcda-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="0dcda-207">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="0dcda-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="0dcda-208">Nella pagina di integrazione dell'applicazione **Salesforce Sandbox** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="0dcda-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="0dcda-209">![Assegnare utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="0dcda-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="0dcda-210">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="0dcda-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="0dcda-211">![Sì](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="0dcda-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="0dcda-212">È ora necessario attendere 10 minuti e verificare che l'account sia stato sincronizzato con Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="0dcda-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="0dcda-213">Per testare le impostazioni di SSO, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0dcda-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="0dcda-214">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0dcda-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

