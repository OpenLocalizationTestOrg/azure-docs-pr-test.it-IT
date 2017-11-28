---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cisco Webex | Documentazione Microsoft'
description: Informazioni su come toouse Cisco Webex con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
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
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="f8fac-103">Esercitazione: Integrazione di Azure Active Directory con Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f8fac-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="f8fac-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f8fac-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="f8fac-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f8fac-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="f8fac-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="f8fac-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f8fac-107">Tenant di Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f8fac-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="f8fac-108">Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooCisco Webex sarà in grado di toosingle sign in un'applicazione hello nel sito della società Cisco Webex (accesso avviato dal provider di servizi su) o tramite hello [toohello introduzione Accedere al pannello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8fac-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="f8fac-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f8fac-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="f8fac-110">Abilitazione hello di integrazione dell'applicazione per Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f8fac-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="f8fac-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="f8fac-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="f8fac-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="f8fac-112">Configuring user provisioning</span></span>
* <span data-ttu-id="f8fac-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="f8fac-113">Assigning users</span></span>

<span data-ttu-id="f8fac-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f8fac-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="f8fac-115">Abilitare l'integrazione dell'applicazione hello per Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="f8fac-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="f8fac-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f8fac-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="f8fac-117">**integrazione dell'applicazione hello tooenable per Cisco Webex, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8fac-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8fac-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f8fac-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f8fac-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f8fac-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="f8fac-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f8fac-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="f8fac-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="f8fac-122">![Applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="f8fac-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f8fac-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f8fac-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="f8fac-124">![Aggiungere un'applicazione](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="f8fac-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f8fac-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="f8fac-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="f8fac-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f8fac-127">In hello **casella di ricerca**, tipo **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="f8fac-128">![Raccolta di applicazioni](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="f8fac-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="f8fac-129">Nel riquadro risultati hello selezionare **Cisco Webex**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f8fac-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="f8fac-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="f8fac-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f8fac-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f8fac-131">Configure single sign-on</span></span>

<span data-ttu-id="f8fac-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCisco Webex con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="f8fac-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="f8fac-133">Come parte di questa procedura, sono toocreate richiesto un certificato con codifica base 64.</span><span class="sxs-lookup"><span data-stu-id="f8fac-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="f8fac-134">Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f8fac-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="f8fac-135">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8fac-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8fac-136">Nel portale di Azure classico, in hello hello **Cisco Webex** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f8fac-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="f8fac-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8fac-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="f8fac-138">In hello **come si sarebbe ad esempio utenti toosign su tooCisco Webex** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f8fac-139">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8fac-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="f8fac-140">In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="f8fac-141">![Configurare l'URL dell'app](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="f8fac-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="f8fac-142">In hello **URL di accesso** casella di testo, digitare l'URL del tenant Cisco Webex (ad esempio: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="f8fac-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="f8fac-143">In hello **URL di risposta Cisco Webex** digitare il **Cisco Webex AssertionConsumerService URL** (ad esempio: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="f8fac-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="f8fac-144">In hello **Configura accesso single sign-on in Cisco Webex** pagina, toodownload il certificato, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f8fac-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="f8fac-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8fac-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="f8fac-146">In un'altra finestra del Web browser accedere al sito aziendale di Cisco Webex come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f8fac-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="f8fac-147">Scegliere dal menu hello in primo piano hello **amministrazione sito**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="f8fac-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span><span class="sxs-lookup"><span data-stu-id="f8fac-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="f8fac-149">In hello **Manage Site** fare clic su **configurazione di SSO**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="f8fac-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="f8fac-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="f8fac-151">Nella sezione di configurazione di SSO Web federata hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8fac-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f8fac-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="f8fac-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="f8fac-153">Da hello **protocollo Federation** elenco, selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="f8fac-154">Creare un file **con codifica Base 64** dal certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="f8fac-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="f8fac-155">Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f8fac-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="f8fac-156">Aprire il certificato con codifica base 64 nel blocco note e quindi hello copia del contenuto di esso.</span><span class="sxs-lookup"><span data-stu-id="f8fac-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="f8fac-157">Fare clic su **Import SAML Metadata**e quindi incollare il certificato con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="f8fac-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="f8fac-158">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **Issuer for SAML (IdP ID)** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8fac-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="f8fac-159">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL accesso remoto** valore e quindi incollarlo hello **Customer SSO Service Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8fac-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="f8fac-160">Da hello **NameID Format** elenco, selezionare **indirizzo di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="f8fac-161">In hello **AuthnContextClassRef** casella tipo **urn: oasis: nomi: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="f8fac-162">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, hello copia **URL disconnessione remota** valore e quindi incollarlo hello **Customer SSO Service Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8fac-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="f8fac-163">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-163">Click **Update**.</span></span>
9. <span data-ttu-id="f8fac-164">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Cisco Webex** nella pagina, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="f8fac-165">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8fac-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="f8fac-166">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="f8fac-166">Configure user provisioning</span></span>

<span data-ttu-id="f8fac-167">In ordine tooenable Azure AD utenti toolog a Cisco Webex, è necessario eseguirne il provisioning in Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="f8fac-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="f8fac-168">Nel caso di hello di Cisco Webex, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f8fac-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="f8fac-169">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="f8fac-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8fac-170">Accedi tooyour **Cisco Webex** tenant.</span><span class="sxs-lookup"><span data-stu-id="f8fac-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="f8fac-171">Andare troppo**Gestisci utenti \> Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="f8fac-172">![Aggiungere utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="f8fac-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="f8fac-173">Nella sezione Aggiungi utente hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8fac-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f8fac-174">![Aggiungere un utente](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="f8fac-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="f8fac-175">Per **Account Type** (Tipo di account), scegliere **Host**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="f8fac-176">Immettere informazioni hello di un utente di Azure AD esistente in hello seguenti caselle di testo: **nome, cognome**, **nome utente**, **posta elettronica**, **Password**, **Conferma Password**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="f8fac-177">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="f8fac-178">È possibile usare qualsiasi altro Cisco Webex utente account strumento di creazione o qualsiasi API fornita da Cisco Webex tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="f8fac-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="f8fac-179">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="f8fac-179">Assign users</span></span>
<span data-ttu-id="f8fac-180">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="f8fac-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="f8fac-181">**gli utenti di tooassign tooCisco Webex, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8fac-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8fac-182">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="f8fac-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f8fac-183">In hello **Cisco Webex** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f8fac-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f8fac-184">![Assegnare utenti](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="f8fac-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="f8fac-185">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="f8fac-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="f8fac-186">![Sì](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="f8fac-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f8fac-187">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="f8fac-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f8fac-188">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8fac-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

