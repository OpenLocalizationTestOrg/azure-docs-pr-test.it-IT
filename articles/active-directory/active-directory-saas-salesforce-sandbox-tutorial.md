---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox | Microsoft Docs'
description: Informazioni su come toouse Salesforce Sandbox con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro.
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
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="d93e5-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="d93e5-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="d93e5-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="d93e5-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="d93e5-105">Per commenti e suggerimenti, vedere hello [pagina di supporto tecnico di Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="d93e5-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="d93e5-106">Concedere sandbox hello possibilità toocreate più copie della propria organizzazione in ambienti separati per diversi scopi, ad esempio sviluppo, testing e training, senza compromettere i dati hello e nelle applicazioni di produzione Salesforce organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="d93e5-107">Per ulteriori informazioni, vedere [Panoramica di Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="d93e5-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="d93e5-108">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d93e5-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d93e5-109">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="d93e5-109">A valid Azure subscription</span></span>
* <span data-ttu-id="d93e5-110">Sandbox in Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="d93e5-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="d93e5-111">Se non si dispone di un ambiente sandbox valido in Salesforce.com, è necessario toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d93e5-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="d93e5-112">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d93e5-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="d93e5-113">Abilitazione hello di integrazione dell'applicazione per Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="d93e5-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="d93e5-114">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d93e5-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d93e5-115">Abilitazione del dominio</span><span class="sxs-lookup"><span data-stu-id="d93e5-115">Enabling your domain</span></span>
4. <span data-ttu-id="d93e5-116">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="d93e5-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="d93e5-117">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="d93e5-117">Assigning users</span></span>

<span data-ttu-id="d93e5-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d93e5-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="d93e5-119">Abilitare l'integrazione dell'applicazione hello per Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="d93e5-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="d93e5-120">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Salesforce sandbox.</span><span class="sxs-lookup"><span data-stu-id="d93e5-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="d93e5-121">**integrazione dell'applicazione hello tooenable per Salesforce sandbox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d93e5-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d93e5-122">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d93e5-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d93e5-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d93e5-124">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="d93e5-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d93e5-125">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="d93e5-126">![Applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="d93e5-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d93e5-127">hello tooopen **raccolta di applicazioni**, fare clic su **Aggiungi un'App**, quindi fare clic su **aggiungere un'applicazione per my toouse organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="d93e5-128">![Cosa si desidera toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Cosa si desidera toodo?")</span><span class="sxs-lookup"><span data-stu-id="d93e5-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="d93e5-129">In hello **casella di ricerca**, tipo **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="d93e5-130">![Raccolta di applicazioni](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="d93e5-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="d93e5-131">Nel riquadro risultati hello selezionare **Salesforce Sandbox**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="d93e5-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="d93e5-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="d93e5-133">Configurare l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d93e5-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="d93e5-134">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSalesforce con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="d93e5-135">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d93e5-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d93e5-136">Nel portale di Azure classico, in hello hello **Salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d93e5-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d93e5-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d93e5-138">In hello **come si sarebbe ad esempio utenti toosign su tooSalesforce Sandbox** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d93e5-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="d93e5-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="d93e5-140">In hello **Configura URL App** pagina hello **URL di accesso** casella di testo, digitare l'URL usando hello modello `http://company.my.salesforce.com`e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="d93e5-141">![Configurare l'URL dell'app](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="d93e5-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="d93e5-142">Se già stato configurato single sign-on per un'altra istanza di Salesforce Sandbox nella directory, quindi è necessario configurare anche hello **identificatore** toohave hello stesso valore di hello **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="d93e5-143">Hello **identificatore** trovato controllando hello **Mostra impostazioni avanzate** casella di controllo hello **Configura URL App** pagina della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="d93e5-144">In hello **Configura accesso single sign-on in Salesforce Sandbox** pagina, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d93e5-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="d93e5-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d93e5-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="d93e5-146">In un'altra finestra del Web browser accedere al sito aziendale di Salesforce Sandbox come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d93e5-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="d93e5-147">Scegliere dal menu hello in primo piano hello **installazione**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="d93e5-148">![Installazione](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="d93e5-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="d93e5-149">Nel riquadro di spostamento hello hello sinistra, fare clic su **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="d93e5-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="d93e5-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="d93e5-151">Nella sezione Impostazioni di Single Sign-On hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d93e5-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d93e5-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="d93e5-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="d93e5-153">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="d93e5-154">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-154">Click **New**.</span></span>
10. <span data-ttu-id="d93e5-155">Nella sezione SAML Single Sign-On Settings hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d93e5-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="d93e5-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="d93e5-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="d93e5-157">Nella casella di testo Nome hello, digitare il nome di hello della configurazione di hello (ad esempio: *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="d93e5-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="d93e5-158">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Salesforce Sandbox** pagina finestra di dialogo, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **dell'autorità di certificazione**casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="d93e5-159">In hello **Id entità** casella tipo **https://test.salesforce.com** se si tratta di hello prima Salesforce Sandbox istanza che si sta aggiungendo tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="d93e5-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="d93e5-160">Se esiste già un'istanza di Salesforce Sandbox, quindi per hello **ID entità** tipo di hello **URL di accesso**, che deve essere nel formato seguente:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d93e5-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="d93e5-161">Fare clic su **Sfoglia** hello tooupload scaricato certificato.</span><span class="sxs-lookup"><span data-stu-id="d93e5-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="d93e5-162">Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="d93e5-163">Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="d93e5-164">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Salesforce Sandbox** pagina finestra di dialogo, hello copia **URL accesso remoto** valore e quindi incollarlo hello **Provider di identità URL di accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="d93e5-165">SFDC non supporta la disconnessione SAML.</span><span class="sxs-lookup"><span data-stu-id="d93e5-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="d93e5-166">In alternativa, incollare 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' in hello **Identity Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="d93e5-167">In **Service Provider Initiated Request Binding** (Binding richiesta avviato dal provider di servizi) selezionare **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="d93e5-168">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-168">Click **Save**.</span></span>
11. <span data-ttu-id="d93e5-169">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="d93e5-170">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d93e5-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="d93e5-171">Abilitare il dominio</span><span class="sxs-lookup"><span data-stu-id="d93e5-171">Enable your domain</span></span>
<span data-ttu-id="d93e5-172">In questa sezione si presuppone che sia già stato creato un dominio.</span><span class="sxs-lookup"><span data-stu-id="d93e5-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="d93e5-173">Per informazioni dettagliate, vedere [Definizione del nome di dominio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="d93e5-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="d93e5-174">**tooenable il dominio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d93e5-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="d93e5-175">Nel riquadro di spostamento a sinistra di hello, fare clic su **Gestione dominio**, quindi fare clic su **risorse del dominio.**</span><span class="sxs-lookup"><span data-stu-id="d93e5-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="d93e5-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="d93e5-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d93e5-177">Assicurarsi che il dominio sia stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="d93e5-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="d93e5-178">In hello **Login Page Settings** fare clic su **modifica**, quindi, come **servizio di autenticazione**, selezionare il nome di hello di hello impostazione SAML Single Sign-On da hello precedente sezione e infine fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="d93e5-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="d93e5-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="d93e5-180">Non appena si dispone di un dominio configurato, gli utenti devono usare Salesforce sandbox di hello dominio URL toologin toohello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="d93e5-181">valore di hello tooget dell'URL di hello, selezionare il profilo SSO hello creato nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="d93e5-182">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="d93e5-182">Configure user provisioning</span></span>
<span data-ttu-id="d93e5-183">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="d93e5-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="d93e5-184">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d93e5-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d93e5-185">Nel portale Salesforce hello, nella barra di spostamento superiore hello, selezionare il nome tooexpand nel menu utente:</span><span class="sxs-lookup"><span data-stu-id="d93e5-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="d93e5-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="d93e5-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="d93e5-187">Nel menu utente selezionare **impostazioni personali** tooopen il **impostazioni personali** pagina.</span><span class="sxs-lookup"><span data-stu-id="d93e5-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="d93e5-188">Nel riquadro di sinistra hello, fare clic su **personale** tooexpand hello sezione personale e quindi fare clic su **Reimposta Token di sicurezza personale**:</span><span class="sxs-lookup"><span data-stu-id="d93e5-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="d93e5-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span><span class="sxs-lookup"><span data-stu-id="d93e5-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="d93e5-190">In hello **Reimposta Token di sicurezza personale** pagina, fare clic su **Reimposta Token di sicurezza** toorequest un messaggio di posta elettronica che contiene il token di sicurezza di Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="d93e5-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="d93e5-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span><span class="sxs-lookup"><span data-stu-id="d93e5-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="d93e5-192">Verificare nella cartella Posta in arrivo la presenza di un messaggio da Salesforce.com con oggetto analogo a "**conferma di sicurezza di salesforce.com.com**".</span><span class="sxs-lookup"><span data-stu-id="d93e5-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="d93e5-193">Esaminare il messaggio di posta elettronica e copia hello sicurezza valore del token.</span><span class="sxs-lookup"><span data-stu-id="d93e5-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="d93e5-194">Nel portale di Azure classico, in hello hello **salesforce Sandbox** pagina di integrazione dell'applicazione, fare clic su **Configura provisioning utente** tooopen hello **Configura Provisioning utente**finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d93e5-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="d93e5-195">![Configurare il provisioning degli utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurare il provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="d93e5-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="d93e5-196">In hello **immettere il Salesforce Sandbox credenziali tooenable il provisioning utente automatico** fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="d93e5-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="d93e5-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="d93e5-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="d93e5-198">In hello **nome utente di amministratore Sandbox Salesforce** casella di testo, tipo di un ambiente sandbox Salesforce nome account a cui è hello **amministratore di sistema** profilo in Salesforce.com assegnato.</span><span class="sxs-lookup"><span data-stu-id="d93e5-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="d93e5-199">In hello **Password amministratore Salesforce Sandbox** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="d93e5-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="d93e5-200">In hello **Token di sicurezza utente** casella valore del token di sicurezza hello Incolla.</span><span class="sxs-lookup"><span data-stu-id="d93e5-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="d93e5-201">Fare clic su **convalida** tooverify la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="d93e5-202">Fare clic su hello **Avanti** hello tooopen pulsante **conferma** pagina.</span><span class="sxs-lookup"><span data-stu-id="d93e5-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="d93e5-203">In hello **conferma** pagina, fare clic su **completa** toosave la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="d93e5-204">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="d93e5-204">Assigning users</span></span>

<span data-ttu-id="d93e5-205">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d93e5-206">**gli utenti di tooassign tooSalesforce Sandbox, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d93e5-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d93e5-207">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="d93e5-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d93e5-208">In hello * * Salesforce Sandbox * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d93e5-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d93e5-209">![Assegnare utenti](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="d93e5-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="d93e5-210">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d93e5-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="d93e5-211">![Sì](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="d93e5-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d93e5-212">È ora necessario attendere 10 minuti e verificare che l'account di hello sia stato sincronizzato tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="d93e5-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="d93e5-213">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="d93e5-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="d93e5-214">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d93e5-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

