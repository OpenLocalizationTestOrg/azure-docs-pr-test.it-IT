---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs'
description: Informazioni su come toouse SAP HANA Cloud Platform con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="8bd51-103">Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8bd51-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="8bd51-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="8bd51-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8bd51-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="8bd51-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="8bd51-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8bd51-107">Account di SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8bd51-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="8bd51-108">Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooSAP HANA Cloud Platform sarà toosingle in grado di accesso in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8bd51-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="8bd51-109">È necessario toodeploy la propria applicazione o la sottoscrizione tooan applicazione sulla piattaforma SAP HANA Cloud singolo tootest di account di accesso.</span><span class="sxs-lookup"><span data-stu-id="8bd51-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="8bd51-110">In questa esercitazione, un'applicazione viene distribuita nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="8bd51-111">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8bd51-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="8bd51-112">Abilitare l'integrazione dell'applicazione hello per SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8bd51-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="8bd51-113">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="8bd51-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8bd51-114">Assegnazione di un utente tooa ruolo</span><span class="sxs-lookup"><span data-stu-id="8bd51-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="8bd51-115">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="8bd51-115">Assigning users</span></span>

<span data-ttu-id="8bd51-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="8bd51-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="8bd51-117">Abilitare l'integrazione dell'applicazione hello per SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8bd51-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="8bd51-118">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="8bd51-119">**integrazione dell'applicazione hello tooenable per SAP HANA Cloud Platform, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8bd51-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bd51-120">In hello portale di gestione di Azure, nel riquadro di spostamento a sinistra di hello, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="8bd51-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8bd51-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8bd51-122">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="8bd51-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8bd51-123">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="8bd51-124">![Applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="8bd51-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8bd51-125">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="8bd51-126">![Aggiungere un'applicazione](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="8bd51-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8bd51-127">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="8bd51-128">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="8bd51-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8bd51-129">In hello **casella di ricerca**, tipo **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="8bd51-130">![Raccolta di applicazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="8bd51-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="8bd51-131">Nel riquadro risultati hello selezionare **SAP HANA Cloud Platform**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="8bd51-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="8bd51-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8bd51-133">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8bd51-133">Configure single sign-on</span></span>

<span data-ttu-id="8bd51-134">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSAP HANA Cloud Platform con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="8bd51-135">Come parte di questa procedura, è necessario tooupload un tenant di SAP HANA Cloud Platform tooyour certificato con codifica base 64.</span><span class="sxs-lookup"><span data-stu-id="8bd51-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="8bd51-136">Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="8bd51-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="8bd51-137">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8bd51-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bd51-138">Nel portale di Azure classico, in hello hello **SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8bd51-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8bd51-139">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8bd51-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="8bd51-140">In hello **come si sarebbe ad esempio utenti toosign su tooSAP HANA Cloud Platform** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8bd51-141">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8bd51-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8bd51-142">In una finestra del web browser, accedere toohello SAP HANA Cloud Platform Cockpit all'https://account. \<host orizzontale\>.ondemand.com/cockpit (ad esempio: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="8bd51-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="8bd51-143">Fare clic su hello **Trust** scheda.</span><span class="sxs-lookup"><span data-stu-id="8bd51-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="8bd51-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="8bd51-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="8bd51-145">Nella sezione Gestione trust eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8bd51-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8bd51-146">![Ottenere i metadati](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Ottenere i metadati")</span><span class="sxs-lookup"><span data-stu-id="8bd51-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="8bd51-147">Fare clic su hello **Local Service Provider** scheda.</span><span class="sxs-lookup"><span data-stu-id="8bd51-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="8bd51-148">Fare clic su hello toodownload file di metadati di SAP HANA Cloud Platform, **Get Metadata**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="8bd51-149">In hello Azure attiva portale classico, in hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="8bd51-150">![Configurare l'URL dell'app](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="8bd51-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="8bd51-151">In hello **URL di accesso** hello digitare l'URL usato dal toosign gli utenti nella casella del **SAP HANA Cloud Platform** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8bd51-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="8bd51-152">Si tratta hello URL specifico per l'account di una risorsa protetta nell'applicazione SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="8bd51-153">Hello URL si basa sul modello di hello: *https://\<applicationName\>\<accountName\>.\< host orizzontale\>.ondemand.com/\<percorso\_a\_protetti\_risorse\>*  (ad esempio: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="8bd51-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="8bd51-154">Si tratta hello URL dell'applicazione SAP HANA Cloud Platform che richiede tooauthenticate utente hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="8bd51-155">Aprire file di metadati di SAP HANA Cloud Platform scaricato hello e individuare hello **NS3: assertionconsumerservice** tag.</span><span class="sxs-lookup"><span data-stu-id="8bd51-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="8bd51-156">Copiare il valore di hello di hello **percorso** attributo e quindi incollarlo hello **SAP HANA Cloud Platform Reply URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8bd51-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="8bd51-157">In hello **Configura accesso single sign-on in SAP HANA Cloud Platform** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8bd51-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="8bd51-158">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8bd51-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="8bd51-159">In SAP HANA Cloud Platform Cockpit Ciao hello **Local Service Provider** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8bd51-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8bd51-160">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="8bd51-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="8bd51-161">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="8bd51-162">In **Configuration Type** selezionare **Custom**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="8bd51-163">Come **Local Provider Name**, lasciare il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="8bd51-164">toogenerate un **chiave per la firma** e **certificato di firma** coppia di chiavi, fare clic su **Generate Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="8bd51-165">In **Propagazione entità** selezionare **Disabilitato**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="8bd51-166">In **Force Authentication** selezionare **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="8bd51-167">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-167">Click **Save**.</span></span>

9. <span data-ttu-id="8bd51-168">Fare clic su hello **Trusted Identity Provider** scheda e quindi fare clic su **Add Trusted Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="8bd51-169">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="8bd51-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="8bd51-170">elenco di hello toomanage dei provider di identità attendibile, è necessario toohave scelto per il tipo di configurazione personalizzata hello hello sezione Local Service Provider.</span><span class="sxs-lookup"><span data-stu-id="8bd51-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="8bd51-171">Per il tipo di configurazione predefinito, è necessario toohello una relazione di trust implicita e non modificabile SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="8bd51-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="8bd51-172">Per Nessuno, non sono disponibili impostazioni di trust.</span><span class="sxs-lookup"><span data-stu-id="8bd51-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="8bd51-173">Fare clic su hello **generale** scheda e quindi fare clic su **Sfoglia** hello tooupload scaricato i file di metadati.</span><span class="sxs-lookup"><span data-stu-id="8bd51-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="8bd51-174">![Gestione dell'attendibilità](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Gestione dell'attendibilità")</span><span class="sxs-lookup"><span data-stu-id="8bd51-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="8bd51-175">Dopo aver caricato il file di metadati hello, hello i valori del parametro **URL servizio Single Sign-on**, **Single Logout URL** e **certificato di firma** vengono popolati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8bd51-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="8bd51-176">Fare clic su hello **attributi** scheda.</span><span class="sxs-lookup"><span data-stu-id="8bd51-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="8bd51-177">In hello **attributi** effettuare hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="8bd51-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="8bd51-178">![Attributi](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="8bd51-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="8bd51-179">Fare clic su **Assertion attributo**, quindi aggiungere hello gli attributi basati su asserzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="8bd51-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="8bd51-180">Attributo di asserzione</span><span class="sxs-lookup"><span data-stu-id="8bd51-180">Assertion Attribute</span></span> | <span data-ttu-id="8bd51-181">Attributo di entità</span><span class="sxs-lookup"><span data-stu-id="8bd51-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="8bd51-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="8bd51-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="8bd51-183">firstname</span><span class="sxs-lookup"><span data-stu-id="8bd51-183">firstname</span></span> |
    | <span data-ttu-id="8bd51-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="8bd51-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="8bd51-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="8bd51-185">lastname</span></span> |
    | <span data-ttu-id="8bd51-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="8bd51-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="8bd51-187">email</span><span class="sxs-lookup"><span data-stu-id="8bd51-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="8bd51-188">configurazione di Hello di hello attributi dipende dalla modalità hello applicazioni in HCP vengono sviluppati, ad esempio quali sono gli attributi previsti nella risposta SAML hello e con quale nome (attributo entità) accedono all'attributo nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="8bd51-189">Hello **l'attributo predefinito** in hello schermata è solo a scopo illustrativo.</span><span class="sxs-lookup"><span data-stu-id="8bd51-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="8bd51-190">Non è richiesto di lavoro di uno scenario toomake hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="8bd51-191">Hello nomi e valori per **Principal Attribute** nell'hello schermata dipendono dalla modalità di sviluppo di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="8bd51-192">È possibile che l'applicazione richieda mapping diversi.</span><span class="sxs-lookup"><span data-stu-id="8bd51-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="8bd51-193">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in SAP HANA Cloud Platform** finestra di dialogo pagina, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="8bd51-194">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8bd51-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="8bd51-195">Gruppi basati su asserzione</span><span class="sxs-lookup"><span data-stu-id="8bd51-195">Assertion-based groups</span></span>
<span data-ttu-id="8bd51-196">Come passaggio facoltativo, è possibile configurare gruppi basati su asserzione per il provider di identità Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bd51-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="8bd51-197">L'utilizzo di gruppi in SAP HANA Cloud Platform consente di assegnare toodynamically uno o più utenti tooone o più ruoli nelle applicazioni SAP HANA Cloud Platform, determinato dai valori di attributi in hello SAML 2.0 asserzione.</span><span class="sxs-lookup"><span data-stu-id="8bd51-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="8bd51-198">Ad esempio, se hello l'asserzione contiene attributi hello "*contratto = temporanea*", si consiglia di tutti gli utenti interessati toobe toohello aggiunto gruppo"*TEMPORANEO*".</span><span class="sxs-lookup"><span data-stu-id="8bd51-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="8bd51-199">gruppo Hello "*TEMPORANEO*" può contenere uno o più ruoli da uno o più applicazioni distribuite nell'account di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="8bd51-200">Utilizzare i gruppi basati su asserzione quando si desidera assegnare toosimultaneously molti utenti tooone o più ruoli di applicazioni nell'account di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="8bd51-201">Se si desidera tooassign solo un singolo o piccolo numero di utenti toospecific ruoli, si consiglia di assegnarli direttamente in hello "**autorizzazioni**" scheda di SAP HANA Cloud Platform cockpit di hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="8bd51-202">Assegnare un utente tooa ruolo</span><span class="sxs-lookup"><span data-stu-id="8bd51-202">Assign a role tooa user</span></span>
<span data-ttu-id="8bd51-203">In ordine tooenable Azure AD utenti toolog a SAP HANA Cloud Platform, è necessario assegnare i ruoli in hello toothem di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8bd51-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="8bd51-204">**tooassign utente tooa un ruolo, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8bd51-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bd51-205">Accedi tooyour **SAP HANA Cloud Platform** Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="8bd51-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="8bd51-206">Eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="8bd51-206">Perform hello following:</span></span>
   
   <span data-ttu-id="8bd51-207">![Autorizzazioni](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizzazioni")</span><span class="sxs-lookup"><span data-stu-id="8bd51-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="8bd51-208">Fare clic su **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="8bd51-209">Fare clic su hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="8bd51-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="8bd51-210">In hello **utente** casella Indirizzo di posta elettronica dell'utente di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="8bd51-211">Fare clic su **assegnare** ruolo tooa di tooassign hello utente.</span><span class="sxs-lookup"><span data-stu-id="8bd51-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="8bd51-212">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="8bd51-213">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="8bd51-213">Assign users</span></span>
<span data-ttu-id="8bd51-214">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="8bd51-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="8bd51-215">**gli utenti di tooassign tooSAP HANA Cloud Platform, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8bd51-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="8bd51-216">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="8bd51-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8bd51-217">In hello **SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8bd51-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="8bd51-218">![Assegnare utenti](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="8bd51-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="8bd51-219">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="8bd51-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="8bd51-220">![Sì](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="8bd51-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8bd51-221">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="8bd51-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="8bd51-222">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8bd51-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

