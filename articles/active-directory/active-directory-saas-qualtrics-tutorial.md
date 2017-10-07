---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qualtrics | Documentazione Microsoft'
description: Informazioni su come toouse Qualtrics con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="d49bd-103">Esercitazione: Integrazione di Azure Active Directory con Qualtrics</span><span class="sxs-lookup"><span data-stu-id="d49bd-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="d49bd-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="d49bd-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="d49bd-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d49bd-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d49bd-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="d49bd-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d49bd-107">Sottoscrizione di Qualtrics abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d49bd-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="d49bd-108">Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooQualtrics saranno in grado di toosingle sign applicazione hello nel sito della società Qualtrics (accesso avviato dal provider di servizi su) o tramite hello [toohello introduzione Accedere al pannello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d49bd-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d49bd-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d49bd-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="d49bd-110">Abilitazione hello di integrazione dell'applicazione per Qualtrics</span><span class="sxs-lookup"><span data-stu-id="d49bd-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="d49bd-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d49bd-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d49bd-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="d49bd-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d49bd-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="d49bd-113">Assigning users</span></span>

<span data-ttu-id="d49bd-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d49bd-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="d49bd-115">Abilitazione hello di integrazione dell'applicazione per Qualtrics</span><span class="sxs-lookup"><span data-stu-id="d49bd-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="d49bd-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione per Qualtrics tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="d49bd-117">**integrazione dell'applicazione hello tooenable per Qualtrics, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d49bd-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="d49bd-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d49bd-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d49bd-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d49bd-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="d49bd-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d49bd-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="d49bd-122">![Applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="d49bd-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d49bd-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="d49bd-124">![Aggiungere un'applicazione](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="d49bd-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d49bd-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="d49bd-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="d49bd-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d49bd-127">In hello **casella di ricerca**, tipo **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="d49bd-128">![Raccolta di applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="d49bd-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="d49bd-129">Nel riquadro risultati hello selezionare **Qualtrics**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="d49bd-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="d49bd-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d49bd-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d49bd-131">Configure single sign-on</span></span>

<span data-ttu-id="d49bd-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooQualtrics con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="d49bd-133">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d49bd-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d49bd-134">Nel portale di Azure classico, in hello hello **Qualtrics** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d49bd-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d49bd-135">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d49bd-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="d49bd-136">In hello **come si sarebbe ad esempio utenti toosign su tooQualtrics** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d49bd-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d49bd-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="d49bd-138">In hello **Configura URL App** hello della pagina **URL accesso Qualtrics** casella di testo, digitare l'URL (ad esempio: "*https://ssotest2ut1.qualtrics.com*"), quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="d49bd-139">![Configurare l'URL dell'app](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="d49bd-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="d49bd-140">In hello **Configura accesso single sign-on in Qualtrics** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d49bd-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="d49bd-141">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d49bd-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="d49bd-142">Inviare hello metadati file toohello team di supporto di Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="d49bd-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d49bd-143">configurazione di SSO Hello è toobe eseguita dal team di supporto di Qualtrics hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="d49bd-144">Si riceverà una notifica non appena la configurazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="d49bd-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="d49bd-145">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d49bd-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="d49bd-146">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d49bd-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="d49bd-147">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="d49bd-147">Configure user provisioning</span></span>

<span data-ttu-id="d49bd-148">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="d49bd-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="d49bd-149">Quando un utente assegnato tenta toolog a Qualtrics mediante il pannello di accesso di hello, Qualtrics verifica se hello utente esiste.</span><span class="sxs-lookup"><span data-stu-id="d49bd-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="d49bd-150">Se l’account utente non è disponibile, viene creato automaticamente da Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="d49bd-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="d49bd-151">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="d49bd-151">Assign users</span></span>
<span data-ttu-id="d49bd-152">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d49bd-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d49bd-153">**tooassign tooQualtrics di utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d49bd-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="d49bd-154">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="d49bd-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d49bd-155">In hello **Qualtrics** pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d49bd-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d49bd-156">![Assegnare utenti](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="d49bd-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="d49bd-157">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d49bd-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="d49bd-158">![Sì](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="d49bd-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d49bd-159">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="d49bd-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="d49bd-160">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d49bd-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

