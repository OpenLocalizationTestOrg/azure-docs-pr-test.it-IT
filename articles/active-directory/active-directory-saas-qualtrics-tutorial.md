---
title: 'Esercitazione: Integrazione di Azure Active Directory con Qualtrics | Documentazione Microsoft'
description: Informazioni su come usare Qualtrics con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
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
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="8f742-103">Esercitazione: Integrazione di Azure Active Directory con Qualtrics</span><span class="sxs-lookup"><span data-stu-id="8f742-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="8f742-104">In questa esercitazione viene illustrata l'integrazione di Azure e Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="8f742-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8f742-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="8f742-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="8f742-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8f742-107">Sottoscrizione di Qualtrics abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="8f742-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8f742-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Qualtrics saranno in grado di eseguire l’accesso Single Sign-On all'applicazione tramite il sito aziendale di Qualtrics (accesso avviato dal provider di servizi) o seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f742-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8f742-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f742-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="8f742-110">Abilitazione dell'integrazione dell'applicazione per Qualtrics</span><span class="sxs-lookup"><span data-stu-id="8f742-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="8f742-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="8f742-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8f742-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="8f742-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8f742-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="8f742-113">Assigning users</span></span>

<span data-ttu-id="8f742-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="8f742-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="8f742-115">Abilitazione dell'integrazione dell'applicazione per Qualtrics</span><span class="sxs-lookup"><span data-stu-id="8f742-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="8f742-116">In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="8f742-117">**Per abilitare l'integrazione dell'applicazione per Qualtrics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f742-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="8f742-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="8f742-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="8f742-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8f742-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8f742-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="8f742-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8f742-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="8f742-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="8f742-122">![Applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="8f742-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8f742-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="8f742-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="8f742-124">![Aggiungere un'applicazione](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="8f742-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8f742-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="8f742-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="8f742-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="8f742-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8f742-127">Nella **casella di ricerca** digitare **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="8f742-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="8f742-128">![Raccolta di applicazioni](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="8f742-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="8f742-129">Nel riquadro dei risultati selezionare **Qualtrics**, quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f742-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="8f742-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="8f742-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8f742-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8f742-131">Configure single sign-on</span></span>

<span data-ttu-id="8f742-132">In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a Qualtrics tramite il proprio account di Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="8f742-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="8f742-133">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f742-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="8f742-134">Nella pagina di integrazione dell'applicazione **Qualtrics** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8f742-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8f742-135">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8f742-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="8f742-136">Nella pagina **Stabilire come si desidera che gli utenti accedano a Qualtrics** selezionare **Single Sign-On di Microsoft Azure AD**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8f742-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="8f742-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8f742-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8f742-138">Nella pagina **Configura URL app** digitare l'URL nella casella di testo **Qualtrics Sign On URL** (URL di accesso a Qualtrics) ad esempio "*https://ssotest2ut1.qualtrics.com*", quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8f742-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="8f742-139">![Configurare l'URL dell'app](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="8f742-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="8f742-140">Nella pagina **Configura accesso Single Sign-On in Qualtrics** fare clic su **Scarica metadati**, quindi salvare il file di metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="8f742-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="8f742-141">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8f742-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="8f742-142">Inviare il file di metadati al team di supporto di Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8f742-143">La configurazione dell'accesso SSO deve essere eseguita dal team di supporto di Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="8f742-144">Al termine della configurazione, viene ricevuta una notifica.</span><span class="sxs-lookup"><span data-stu-id="8f742-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="8f742-145">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="8f742-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8f742-146">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8f742-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="8f742-147">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="8f742-147">Configure user provisioning</span></span>

<span data-ttu-id="8f742-148">Non è richiesto alcun intervento dell'utente per configurare il provisioning degli utenti in Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="8f742-149">Quando un utente assegnato tenta di accedere a Qualtrics usando il pannello di accesso, Qualtrics verifica se l'utente esiste.</span><span class="sxs-lookup"><span data-stu-id="8f742-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="8f742-150">Se l’account utente non è disponibile, viene creato automaticamente da Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="8f742-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="8f742-151">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="8f742-151">Assign users</span></span>
<span data-ttu-id="8f742-152">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f742-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="8f742-153">**Per assegnare gli utenti a Qualtrics, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="8f742-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="8f742-154">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="8f742-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8f742-155">Nella pagina di integrazione dell'applicazione **Qualtrics** fare clic su **Assegna utenti**.</span><span class="sxs-lookup"><span data-stu-id="8f742-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="8f742-156">![Assegnare utenti](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="8f742-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="8f742-157">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="8f742-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="8f742-158">![Sì](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="8f742-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8f742-159">Per testare le impostazioni di SSO, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8f742-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="8f742-160">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f742-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

