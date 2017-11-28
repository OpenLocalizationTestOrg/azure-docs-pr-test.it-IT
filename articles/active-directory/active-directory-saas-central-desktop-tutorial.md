---
title: 'Esercitazione: Integrazione di Azure Active Directory con Central Desktop | Documentazione Microsoft'
description: Informazioni su come toouse Central Desktop con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
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
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="f8dc0-103">Esercitazione: Integrazione di Azure Active Directory con Central Desktop</span><span class="sxs-lookup"><span data-stu-id="f8dc0-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="f8dc0-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="f8dc0-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="f8dc0-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="f8dc0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="f8dc0-107">Sottoscrizione di Central Desktop abilitata per l'accesso Single Sign-On e tenant di Central Desktop</span><span class="sxs-lookup"><span data-stu-id="f8dc0-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="f8dc0-108">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="f8dc0-109">Abilitazione hello di integrazione dell'applicazione per Central Desktop</span><span class="sxs-lookup"><span data-stu-id="f8dc0-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="f8dc0-110">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="f8dc0-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="f8dc0-111">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="f8dc0-111">Configuring user provisioning</span></span>
* <span data-ttu-id="f8dc0-112">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="f8dc0-112">Assigning users</span></span>

<span data-ttu-id="f8dc0-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="f8dc0-114">Abilitare l'integrazione dell'applicazione hello per Central Desktop</span><span class="sxs-lookup"><span data-stu-id="f8dc0-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="f8dc0-115">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="f8dc0-116">**integrazione dell'applicazione hello tooenable per Central Desktop, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-117">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="f8dc0-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="f8dc0-119">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="f8dc0-120">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="f8dc0-121">![Applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="f8dc0-122">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="f8dc0-123">![Aggiungere un'applicazione](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="f8dc0-124">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="f8dc0-125">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="f8dc0-126">In hello **casella di ricerca**, tipo **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="f8dc0-127">![Raccolta di applicazioni](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="f8dc0-128">Nel riquadro risultati hello selezionare **Central Desktop**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="f8dc0-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="f8dc0-130">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f8dc0-130">Configure single sign-on</span></span>

<span data-ttu-id="f8dc0-131">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooCentral Desktop con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="f8dc0-132">Come parte di questa procedura, è necessario tooupload un tenant di Central Desktop tooyour certificato con codifica base 64.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="f8dc0-133">Se non si ha familiarità con questa procedura, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="f8dc0-134">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-135">Nel portale di Azure classico, in hello hello **Central Desktop** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="f8dc0-136">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="f8dc0-137">In hello **come si sarebbe ad esempio utenti toosign su tooCentral Desktop** selezionare **Microsoft Azure AD Single Sign-On**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="f8dc0-138">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="f8dc0-139">In hello **Configura URL App** pagina, eseguire hello alla procedura seguente e quindi fare clic su **Avanti**:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="f8dc0-140">In hello **Central Desktop Sign In URL** casella di testo, hello digitare l'URL del tenant di Central Desktop (ad esempio: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="f8dc0-141">Nella casella di testo URL di risposta Central Desktop hello, digitare l'URL AssertionConsumerService di Central Desktop (ad esempio: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f8dc0-142">È possibile ottenere il valore di hello dai metadati desktop centrale hello (ad esempio: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="f8dc0-143">![Configurare l'URL dell'app](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="f8dc0-144">In hello **Configura accesso single sign-on in Central Desktop** pagina, toodownload il certificato, fare clic su **Scarica certificato**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="f8dc0-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="f8dc0-146">Accedi tooyour **Central Desktop** tenant.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="f8dc0-147">Andare troppo**impostazioni**, fare clic su **avanzate**, quindi fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="f8dc0-148">![Installazione - Avanzate](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Installazione - Avanzate")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="f8dc0-149">In hello **Single Sign On Settings** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="f8dc0-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="f8dc0-151">Selezionare **Enable SAML v2 Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="f8dc0-152">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL autorità di certificazione** valore e quindi incollarlo hello **URL SSO** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="f8dc0-153">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL accesso remoto** valore e quindi incollarlo hello **SSO Login URL**casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="f8dc0-154">Nel portale di Azure classico, in hello hello **Configura accesso single sign-on in Central Desktop** pagina, hello copia **URL del servizio Single Sign-Out** valore e quindi incollarlo hello **URL disconnessione SSO** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="f8dc0-155">In hello **metodo verifica della firma del messaggio** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f8dc0-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="f8dc0-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="f8dc0-157">Selezionare **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="f8dc0-158">Da hello **certificato SSO** elenco, selezionare **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="f8dc0-159">Creare un file di testo dal certificato scaricato hello, hello copia del contenuto del file di testo hello e quindi incollarlo hello **certificato SSO** campo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="f8dc0-160">Per ulteriori informazioni, vedere [come tooconvert certificato di un file binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="f8dc0-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="f8dc0-161">Selezionare **visualizzare una pagina di accesso di SAMLv2 tooyour collegamento**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="f8dc0-162">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-162">Click **Update**.</span></span>
10. <span data-ttu-id="f8dc0-163">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="f8dc0-164">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="f8dc0-165">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="f8dc0-165">Configure user provisioning</span></span>

<span data-ttu-id="f8dc0-166">Per AAD utenti toobe in grado di toosign in devono essere sottoposte a provisioning toohello applicazione Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="f8dc0-167">In questa sezione viene descritto come degli account utente AAD toocreate in Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="f8dc0-168">**gli account utente tooprovision tooCentral Desktop:**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="f8dc0-169">Accedi tooyour tenant di Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="f8dc0-170">Andare troppo**persone \> membri interni**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="f8dc0-171">Fare clic su **Add Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="f8dc0-172">![Persone](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="f8dc0-173">In hello **Email Address of New Members** casella di testo, digitare un account AAD, si desidera tooprovision e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="f8dc0-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="f8dc0-175">Fare clic su **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="f8dc0-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f8dc0-177">gli utenti di Hello aggiunti riceveranno un messaggio di posta elettronica che include un collegamento di conferma account hello di tooclick tooactivate.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="f8dc0-178">È possibile usare qualsiasi altro Central Desktop utente account strumento di creazione o le API fornite da Central Desktop tooprovision account utente di AAD</span><span class="sxs-lookup"><span data-stu-id="f8dc0-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="f8dc0-179">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="f8dc0-179">Assign users</span></span>
<span data-ttu-id="f8dc0-180">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="f8dc0-181">**gli utenti di tooassign tooCentral Desktop, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f8dc0-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8dc0-182">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="f8dc0-183">In hello **Central Desktop** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="f8dc0-184">![Assegnare utenti](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="f8dc0-185">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="f8dc0-186">![Sì](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="f8dc0-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="f8dc0-187">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="f8dc0-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="f8dc0-188">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8dc0-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

