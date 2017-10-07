---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure | Documentazione Microsoft'
description: Informazioni su come toouse TOPdesk - Secure con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e altro ancora!.
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
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="ea508-103">Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="ea508-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="ea508-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="ea508-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="ea508-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ea508-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="ea508-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="ea508-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ea508-107">Sottoscrizione di TOPdesk - Secure abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea508-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="ea508-108">Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooTOPdesk - verrà protetto è in grado di toosingle sign in un'applicazione hello in TOPdesk - sito aziendale protetta (accesso avviato dal provider di servizi su) oppure utilizza hello [introduzione Pannello di accesso toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea508-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="ea508-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ea508-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="ea508-110">Abilitare l'integrazione dell'applicazione hello per TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="ea508-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="ea508-111">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea508-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="ea508-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="ea508-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="ea508-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="ea508-113">Assigning users</span></span>

<span data-ttu-id="ea508-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="ea508-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="ea508-115">Abilitare l'integrazione dell'applicazione hello per TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="ea508-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="ea508-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="ea508-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="ea508-117">integrazione dell'applicazione hello tooenable per TOPdesk - Secure, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="ea508-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea508-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="ea508-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ea508-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="ea508-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="ea508-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="ea508-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="ea508-122">![Applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="ea508-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="ea508-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="ea508-124">![Aggiungere un'applicazione](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="ea508-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="ea508-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="ea508-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="ea508-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="ea508-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="ea508-127">In hello **casella di ricerca**, tipo **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="ea508-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="ea508-128">![Raccolta di applicazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="ea508-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="ea508-129">Nel riquadro risultati hello selezionare **TOPdesk - Secure**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="ea508-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="ea508-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="ea508-131">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea508-131">Configuring single sign-on</span></span>
<span data-ttu-id="ea508-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooTOPdesk - Secure con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="ea508-133">Configurazione single sign-on per TOPdesk - Secure richiede tooupload un file icona del logo.</span><span class="sxs-lookup"><span data-stu-id="ea508-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="ea508-134">file dell'icona hello tooget, team di supporto di TOPdesk hello contatto.</span><span class="sxs-lookup"><span data-stu-id="ea508-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="ea508-135">tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="ea508-136">Accesso tooyour **TOPdesk - Secure** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ea508-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="ea508-137">In hello **TOPdesk** menu, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea508-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="ea508-138">![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="ea508-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="ea508-139">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="ea508-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="ea508-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="ea508-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="ea508-141">Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.</span><span class="sxs-lookup"><span data-stu-id="ea508-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="ea508-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="ea508-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="ea508-143">In hello **sicura** sezione di hello **SAML login** configurazione seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ea508-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="ea508-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="ea508-145">a.</span><span class="sxs-lookup"><span data-stu-id="ea508-145">a.</span></span> <span data-ttu-id="ea508-146">Fare clic su **scaricare** toodownload hello file di metadati pubblici e quindi salvarlo in locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ea508-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="ea508-147">b.</span><span class="sxs-lookup"><span data-stu-id="ea508-147">b.</span></span> <span data-ttu-id="ea508-148">Aprire il file di metadati hello e individuare hello **AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="ea508-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="ea508-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="ea508-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="ea508-150">c.</span><span class="sxs-lookup"><span data-stu-id="ea508-150">c.</span></span> <span data-ttu-id="ea508-151">Hello copia **AssertionConsumerService** valore.</span><span class="sxs-lookup"><span data-stu-id="ea508-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="ea508-152">Si sarà necessario hello valore hello **Configura URL App** sezione più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ea508-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="ea508-153">In un'altra finestra del Web browser accedere al portale di **portale di Azure classico** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ea508-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="ea508-154">In hello **TOPdesk - Secure** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ea508-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="ea508-155">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ea508-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="ea508-156">In hello **come verrebbe come utenti toosign su tooTOPdesk - Secure** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ea508-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ea508-157">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ea508-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="ea508-158">In hello **Configura URL App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ea508-159">![Configurare l'URL dell'app](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="ea508-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="ea508-160">a.</span><span class="sxs-lookup"><span data-stu-id="ea508-160">a.</span></span> <span data-ttu-id="ea508-161">In hello **TOPdesk - Secure URL di accesso** casella di testo, digitare l'URL hello usato dal toosign gli utenti nell'applicazione TOPdesk - Secure (ad esempio: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="ea508-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="ea508-162">b.</span><span class="sxs-lookup"><span data-stu-id="ea508-162">b.</span></span> <span data-ttu-id="ea508-163">In hello **TOPdesk-URL di risposta pubblica** casella di testo, incollare hello **TOPdesk - Secure AssertionConsumerService URL** (ad esempio: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="ea508-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="ea508-164">c.</span><span class="sxs-lookup"><span data-stu-id="ea508-164">c.</span></span> <span data-ttu-id="ea508-165">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ea508-165">Click **Next**.</span></span>

10. <span data-ttu-id="ea508-166">In hello **Configura accesso single sign-on in TOPdesk - Secure** pagina, toodownload il file di metadati, fare clic su **Scarica metadati**e quindi salvare il file hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="ea508-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="ea508-167">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ea508-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="ea508-168">toocreate un file di certificato, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="ea508-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="ea508-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="ea508-170">a.</span><span class="sxs-lookup"><span data-stu-id="ea508-170">a.</span></span> <span data-ttu-id="ea508-171">File di metadati scaricato hello aperto.</span><span class="sxs-lookup"><span data-stu-id="ea508-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="ea508-172">b.</span><span class="sxs-lookup"><span data-stu-id="ea508-172">b.</span></span> <span data-ttu-id="ea508-173">Espandere hello **RoleDescriptor** nodo che dispone di un **xsi: Type** di **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="ea508-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="ea508-174">c.</span><span class="sxs-lookup"><span data-stu-id="ea508-174">c.</span></span> <span data-ttu-id="ea508-175">Copiare il valore di hello di hello **X509Certificate** nodo.</span><span class="sxs-lookup"><span data-stu-id="ea508-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="ea508-176">d.</span><span class="sxs-lookup"><span data-stu-id="ea508-176">d.</span></span> <span data-ttu-id="ea508-177">Salva hello copiato **X509Certificate** valore in locale nel computer in un file.</span><span class="sxs-lookup"><span data-stu-id="ea508-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="ea508-178">In TOPdesk - Secure hello del sito della società **TOPdesk** menu, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea508-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="ea508-179">![Impostazioni](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="ea508-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="ea508-180">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="ea508-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="ea508-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="ea508-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="ea508-182">Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.</span><span class="sxs-lookup"><span data-stu-id="ea508-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="ea508-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="ea508-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="ea508-184">In hello **pubblica** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ea508-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="ea508-185">![Aggiungi](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="ea508-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="ea508-186">In hello **Assistente configurazione SAML** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="ea508-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="ea508-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="ea508-188">a.</span><span class="sxs-lookup"><span data-stu-id="ea508-188">a.</span></span> <span data-ttu-id="ea508-189">tooupload file i metadati scaricati, in **i metadati della federazione**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="ea508-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="ea508-190">b.</span><span class="sxs-lookup"><span data-stu-id="ea508-190">b.</span></span> <span data-ttu-id="ea508-191">file del certificato, in tooupload **Certificate (RSA)**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="ea508-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="ea508-192">c.</span><span class="sxs-lookup"><span data-stu-id="ea508-192">c.</span></span> <span data-ttu-id="ea508-193">file del logo hello tooupload ottenuto dal team di supporto di TOPdesk hello, in **icona del Logo**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="ea508-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="ea508-194">d.</span><span class="sxs-lookup"><span data-stu-id="ea508-194">d.</span></span> <span data-ttu-id="ea508-195">In hello **attributo nome utente** casella tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="ea508-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="ea508-196">e.</span><span class="sxs-lookup"><span data-stu-id="ea508-196">e.</span></span> <span data-ttu-id="ea508-197">In hello **nome visualizzato** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="ea508-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ea508-198">f.</span><span class="sxs-lookup"><span data-stu-id="ea508-198">f.</span></span> <span data-ttu-id="ea508-199">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ea508-199">Click **Save**.</span></span>

17. <span data-ttu-id="ea508-200">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ea508-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="ea508-201">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ea508-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="ea508-202">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="ea508-202">Configuring user provisioning</span></span>
<span data-ttu-id="ea508-203">In ordine tooenable Azure AD utenti toolog TopDesk - Secure, è necessario eseguirne il provisioning in TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="ea508-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="ea508-204">Nel caso di hello di TOPdesk - Secure, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ea508-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="ea508-205">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="ea508-206">Accesso tooyour **TOPdesk - Secure** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ea508-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="ea508-207">Scegliere dal menu hello in primo piano hello **TOPdesk \> New \> i file di supporto \> operatore**.</span><span class="sxs-lookup"><span data-stu-id="ea508-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="ea508-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="ea508-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="ea508-209">In hello **nuovo operatore** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ea508-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span><span class="sxs-lookup"><span data-stu-id="ea508-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="ea508-211">a.</span><span class="sxs-lookup"><span data-stu-id="ea508-211">a.</span></span> <span data-ttu-id="ea508-212">Fare clic sulla scheda Generale hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="ea508-213">b.</span><span class="sxs-lookup"><span data-stu-id="ea508-213">b.</span></span> <span data-ttu-id="ea508-214">In hello **Surname** casella di testo di hello **generale** sezione, digitare hello cognome di un account Azure Active Directory valido, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="ea508-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="ea508-215">c.</span><span class="sxs-lookup"><span data-stu-id="ea508-215">c.</span></span> <span data-ttu-id="ea508-216">Selezionare un **sito** per conto di hello in hello **percorso** sezione.</span><span class="sxs-lookup"><span data-stu-id="ea508-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="ea508-217">d.</span><span class="sxs-lookup"><span data-stu-id="ea508-217">d.</span></span> <span data-ttu-id="ea508-218">In hello **nome account di accesso** casella di testo di hello **TOPdesk Login** , immettere un nome di account di accesso per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ea508-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="ea508-219">e.</span><span class="sxs-lookup"><span data-stu-id="ea508-219">e.</span></span> <span data-ttu-id="ea508-220">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ea508-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ea508-221">È possibile usare qualsiasi altro - account utente sicura di creazione o le API fornite da TOPdesk - Secure tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="ea508-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="ea508-222">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="ea508-222">Assigning users</span></span>
<span data-ttu-id="ea508-223">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="ea508-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="ea508-224">tooassign utenti tooTOPdesk - Secure, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea508-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="ea508-225">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="ea508-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ea508-226">In hello * * TOPdesk - Secure * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ea508-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="ea508-227">![Assegnare utenti](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="ea508-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="ea508-228">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="ea508-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="ea508-229">![Sì](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="ea508-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ea508-230">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="ea508-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="ea508-231">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea508-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

