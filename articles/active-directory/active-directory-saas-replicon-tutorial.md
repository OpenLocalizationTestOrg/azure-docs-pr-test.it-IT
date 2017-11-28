---
title: 'Esercitazione: Integrazione di Azure Active Directory con Replicon | Documentazione Microsoft'
description: Informazioni su come toouse Replicon con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
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
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="54dcc-103">Esercitazione: Integrazione di Azure Active Directory con Replicon</span><span class="sxs-lookup"><span data-stu-id="54dcc-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="54dcc-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Replicon.</span><span class="sxs-lookup"><span data-stu-id="54dcc-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="54dcc-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="54dcc-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="54dcc-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="54dcc-106">A valid Azure subscription</span></span>
* <span data-ttu-id="54dcc-107">Tenant Replicon</span><span class="sxs-lookup"><span data-stu-id="54dcc-107">A Replicon tenant</span></span>

<span data-ttu-id="54dcc-108">Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooReplicon saranno in grado di toosingle sign applicazione hello nel sito aziendale Replicon (accesso avviato dal provider di servizi su) o tramite hello [introduzione toohello accesso Pannello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54dcc-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="54dcc-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="54dcc-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="54dcc-110">Abilitazione hello di integrazione dell'applicazione per Replicon</span><span class="sxs-lookup"><span data-stu-id="54dcc-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="54dcc-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="54dcc-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="54dcc-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="54dcc-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="54dcc-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="54dcc-113">Assigning users</span></span>

<span data-ttu-id="54dcc-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="54dcc-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="54dcc-115">Abilitare l'integrazione dell'applicazione per Replicon hello</span><span class="sxs-lookup"><span data-stu-id="54dcc-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="54dcc-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione per Replicon tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="54dcc-117">**integrazione dell'applicazione hello tooenable per Replicon, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="54dcc-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="54dcc-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="54dcc-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="54dcc-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="54dcc-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="54dcc-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="54dcc-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="54dcc-122">![Applicazioni](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="54dcc-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="54dcc-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="54dcc-124">![Aggiungere un'applicazione](./media/active-directory-saas-replicon-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="54dcc-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="54dcc-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="54dcc-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-replicon-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="54dcc-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="54dcc-127">In hello **casella di ricerca**, tipo **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="54dcc-128">![Raccolta di applicazioni](./media/active-directory-saas-replicon-tutorial/IC777799.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="54dcc-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="54dcc-129">Nel riquadro risultati hello selezionare **Replicon**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="54dcc-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="54dcc-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="54dcc-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="54dcc-131">Configure single sign-on</span></span>

<span data-ttu-id="54dcc-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooReplicon con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="54dcc-133">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="54dcc-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="54dcc-134">Nel portale di Azure classico, in hello hello **Replicon** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="54dcc-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="54dcc-135">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="54dcc-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="54dcc-136">In hello **come si sarebbe ad esempio utenti toosign su tooReplicon** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="54dcc-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="54dcc-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="54dcc-138">In hello **Configura URL App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="54dcc-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="54dcc-139">![Configurare l'URL dell'app](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="54dcc-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="54dcc-140">In hello **URL di accesso Replicon** casella di testo, digitare l'URL del tenant Replicon (ad esempio: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="54dcc-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="54dcc-141">In hello **URL di risposta Replicon** casella di testo, digitare l'URL **AssertionConsumerService** URL (ad esempio: *https://global.replicon.com/!saml2/aziendale/sso/post/*).</span><span class="sxs-lookup"><span data-stu-id="54dcc-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="54dcc-142">È possibile ottenere l'URL di hello dai metadati di Replicon hello in: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="54dcc-143">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-143">Click **Next**.</span></span>

4. <span data-ttu-id="54dcc-144">In hello **Configura accesso single sign-on in Replicon** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare hello metadati nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="54dcc-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="54dcc-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="54dcc-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="54dcc-146">In un'altra finestra del Web browser accedere al sito aziendale di Replicon come amministratore.</span><span class="sxs-lookup"><span data-stu-id="54dcc-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="54dcc-147">tooconfigure SAML 2.0, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="54dcc-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="54dcc-148">![Abilita autenticazione SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "autenticazione SAML abilitare")</span><span class="sxs-lookup"><span data-stu-id="54dcc-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="54dcc-149">hello toodisplay **EnableSAML Authentication2** finestra di dialogo, aggiungere hello seguente URL di tooyour, dopo la chiave dell'azienda: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="54dcc-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="54dcc-150">Hello il seguente schema hello dell'URL completo di hello:</span><span class="sxs-lookup"><span data-stu-id="54dcc-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="54dcc-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="54dcc-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="54dcc-152">Fare clic su hello  **+**  tooexpand hello **v20Configuration** sezione.</span><span class="sxs-lookup"><span data-stu-id="54dcc-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="54dcc-153">Fare clic su hello  **+**  tooexpand hello **metaDataConfiguration** sezione.</span><span class="sxs-lookup"><span data-stu-id="54dcc-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="54dcc-154">Fare clic su **Scegli File**, tooselect del file XML dei metadati del provider di identità e scegliere **Invia**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="54dcc-155">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="54dcc-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="54dcc-156">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="54dcc-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="54dcc-157">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="54dcc-157">Configure user provisioning</span></span>

<span data-ttu-id="54dcc-158">In ordine tooenable Azure AD utenti toolog a Replicon, è necessario eseguirne il provisioning in Replicon.</span><span class="sxs-lookup"><span data-stu-id="54dcc-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="54dcc-159">Nel caso di hello di Replicon, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="54dcc-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="54dcc-160">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="54dcc-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="54dcc-161">In una finestra del Web browser accedere al sito aziendale di Replicon come amministratore.</span><span class="sxs-lookup"><span data-stu-id="54dcc-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="54dcc-162">Andare troppo**amministrazione \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="54dcc-163">![Utenti](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="54dcc-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="54dcc-164">Fare clic su **+Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="54dcc-165">![Aggiungere un utente](./media/active-directory-saas-replicon-tutorial/IC777807.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="54dcc-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="54dcc-166">In hello **profilo utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="54dcc-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="54dcc-167">![Profilo utente](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profilo utente")</span><span class="sxs-lookup"><span data-stu-id="54dcc-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="54dcc-168">In hello **nome account di accesso** casella di testo, hello tipo AD Azure indirizzo di posta elettronica dell'utente hello Azure AD si vuole tooprovision.</span><span class="sxs-lookup"><span data-stu-id="54dcc-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="54dcc-169">In **Tipo di autenticazione** selezionare **SSO**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="54dcc-170">In hello **reparto** casella di testo, digitare il reparto dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="54dcc-171">In **Tipo di dipendente** selezionare **Amministratore**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="54dcc-172">Fare clic su **Salva profilo utente**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="54dcc-173">È possibile usare qualsiasi altro Replicon utente account strumento di creazione o le API fornite da Replicon tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="54dcc-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="54dcc-174">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="54dcc-174">Assign users</span></span>
<span data-ttu-id="54dcc-175">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="54dcc-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="54dcc-176">**tooassign tooReplicon di utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="54dcc-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="54dcc-177">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="54dcc-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="54dcc-178">In hello **Replicon** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="54dcc-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="54dcc-179">![Assegnare utenti](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="54dcc-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="54dcc-180">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="54dcc-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="54dcc-181">![Sì](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="54dcc-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="54dcc-182">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="54dcc-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="54dcc-183">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54dcc-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

