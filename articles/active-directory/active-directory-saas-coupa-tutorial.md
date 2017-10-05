---
title: 'Esercitazione: Integrazione di Azure Active Directory con Coupa | Documentazione Microsoft'
description: Informazioni su come usare Coupa con Azure Active Directory per abilitare l'accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="a4cac-103">Esercitazione: Integrazione di Azure Active Directory con Coupa</span><span class="sxs-lookup"><span data-stu-id="a4cac-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="a4cac-104">Questa esercitazione descrive l'integrazione di Azure e Coupa.</span><span class="sxs-lookup"><span data-stu-id="a4cac-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="a4cac-105">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a4cac-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="a4cac-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="a4cac-106">A valid Azure subscription</span></span>
* <span data-ttu-id="a4cac-107">Sottoscrizione di Coupa abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="a4cac-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="a4cac-108">Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Coupa potranno eseguire l'accesso Single Sign-On all'applicazione seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4cac-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="a4cac-109">Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4cac-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="a4cac-110">Abilitazione dell'integrazione dell'applicazione per Coupa</span><span class="sxs-lookup"><span data-stu-id="a4cac-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="a4cac-111">Configurazione dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4cac-111">Configuring single sign-on</span></span>
* <span data-ttu-id="a4cac-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="a4cac-112">Configuring user provisioning</span></span>
* <span data-ttu-id="a4cac-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="a4cac-113">Assigning users</span></span>

<span data-ttu-id="a4cac-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="a4cac-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="a4cac-115">Abilitare l'integrazione dell'applicazione per Coupa</span><span class="sxs-lookup"><span data-stu-id="a4cac-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="a4cac-116">Questa sezione descrive come abilitare l'integrazione dell'applicazione per Coupa.</span><span class="sxs-lookup"><span data-stu-id="a4cac-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="a4cac-117">**Per abilitare l'integrazione dell'applicazione per Coupa, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4cac-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="a4cac-118">Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="a4cac-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="a4cac-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="a4cac-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="a4cac-120">Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.</span><span class="sxs-lookup"><span data-stu-id="a4cac-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a4cac-121">Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.</span><span class="sxs-lookup"><span data-stu-id="a4cac-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="a4cac-122">![Applicazioni](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="a4cac-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="a4cac-123">Fare clic su **Add** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="a4cac-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="a4cac-124">![Aggiungere un'applicazione](./media/active-directory-saas-coupa-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="a4cac-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="a4cac-125">Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="a4cac-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-coupa-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="a4cac-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="a4cac-127">Nella **casella di ricerca** digitare **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="a4cac-128">![Raccolta di applicazioni](./media/active-directory-saas-coupa-tutorial/IC791898.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="a4cac-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="a4cac-129">Nel riquadro dei risultati selezionare **Coupa** e quindi fare clic su **Completa** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4cac-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="a4cac-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="a4cac-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="a4cac-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a4cac-131">Configure single sign-on</span></span>

<span data-ttu-id="a4cac-132">Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione ad Coupa tramite il proprio account in Azure AD usando la federazione basata sul protocollo SAML.</span><span class="sxs-lookup"><span data-stu-id="a4cac-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="a4cac-133">La configurazione dell'accesso Single Sign-On per Coupa richiede di recuperare un valore di identificazione personale da un certificato.</span><span class="sxs-lookup"><span data-stu-id="a4cac-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="a4cac-134">Se non si ha familiarità con questa procedura, vedere [Procedura: recuperare l'identificazione personale di un certificato](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="a4cac-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="a4cac-135">**Per configurare l'accesso Single Sign-On, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4cac-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="a4cac-136">Accedere al sito aziendale di Coupa come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4cac-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="a4cac-137">Passare a **Setup (Configurazione) \> Security Control (Controllo di sicurezza)**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="a4cac-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="a4cac-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="a4cac-139">Per scaricare il file dei metadati Coupa nel computer fare clic su **Scarica e importa i metadati SP**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="a4cac-140">![Metadati Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadati Coupa SP")</span><span class="sxs-lookup"><span data-stu-id="a4cac-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="a4cac-141">In un'altra finestra del browser accedere al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a4cac-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="a4cac-142">Nella pagina di integrazione dell'applicazione **Coupa** fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="a4cac-143">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a4cac-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="a4cac-144">Nella pagina **Stabilire come si desidera che gli utenti accedano a Coupa** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="a4cac-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a4cac-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="a4cac-146">Nella pagina **Configura URL app** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4cac-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="a4cac-147">![Configurare l'URL dell'app](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="a4cac-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="a4cac-148">Nella casella di testo **URL di accesso** digitare l'URL usato dagli utenti per accedere all'applicazione Coupa, ad esempio: "*http://company.Coupa.com*".</span><span class="sxs-lookup"><span data-stu-id="a4cac-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="a4cac-149">Aprire il file dei metadati Coupa scaricato e quindi copiare il valore di **Indice/URL AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="a4cac-150">Nella casella di testo **URL di risposta Coupa** incollare il valore di **AssertionConsumerService index/URL** (Indice/URL AssertionConsumerService).</span><span class="sxs-lookup"><span data-stu-id="a4cac-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="a4cac-151">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-151">Click **Next**.</span></span>
8. <span data-ttu-id="a4cac-152">Nella pagina **Configura accesso Single Sign-On in Coupa** fare clic su **Scarica metadati** per scaricare il file di metadati e salvarlo nel computer.</span><span class="sxs-lookup"><span data-stu-id="a4cac-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="a4cac-153">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a4cac-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="a4cac-154">Nel sito aziendale Coupa passare a **Setup (Configurazione) \> Security Control (Controllo di sicurezza)**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="a4cac-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="a4cac-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="a4cac-156">Nella sezione **Accesso mediante le credenziali di Coupa** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4cac-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="a4cac-157">![Accesso mediante le credenziali di Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Accesso mediante le credenziali di Coupa")</span><span class="sxs-lookup"><span data-stu-id="a4cac-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="a4cac-158">Selezionare **Accedere mediante SAML**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="a4cac-159">Fare clic su **Sfoglia** per caricare il file di metadati di Azure Active Directory scaricato.</span><span class="sxs-lookup"><span data-stu-id="a4cac-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="a4cac-160">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-160">Click **Save**.</span></span>
11. <span data-ttu-id="a4cac-161">Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Complete** per chiudere la finestra di dialogo **Configura accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="a4cac-162">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="a4cac-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="a4cac-163">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="a4cac-163">Configure user provisioning</span></span>

<span data-ttu-id="a4cac-164">Per consentire agli utenti di Azure AD di accedere a Coupa, è necessario eseguirne il provisioning in Coupa.</span><span class="sxs-lookup"><span data-stu-id="a4cac-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="a4cac-165">Nel caso di Coupa, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a4cac-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="a4cac-166">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4cac-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a4cac-167">Accedere al sito aziendale di **Coupa** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4cac-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="a4cac-168">Nel menu in alto fare clic su **Setup** (Configura) e quindi su **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="a4cac-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="a4cac-169">![Utenti](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="a4cac-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="a4cac-170">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-170">Click **Create**.</span></span>
   
   <span data-ttu-id="a4cac-171">![Creare utenti](./media/active-directory-saas-coupa-tutorial/IC791909.png "Creare utenti")</span><span class="sxs-lookup"><span data-stu-id="a4cac-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="a4cac-172">Nella sezione **Crea utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4cac-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="a4cac-173">![Dettagli utente](./media/active-directory-saas-coupa-tutorial/IC791910.png "Dettagli utente")</span><span class="sxs-lookup"><span data-stu-id="a4cac-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="a4cac-174">Nelle caselle **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** immettere l'account di accesso, il nome, il cognome, l'ID Single Sign-On e l'indirizzo di posta elettronica di un account Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a4cac-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="a4cac-175">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="a4cac-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="a4cac-176">Il titolare dell'account Azure Active Directory riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="a4cac-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="a4cac-177">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Coupa per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="a4cac-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="a4cac-178">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="a4cac-178">Assign users</span></span>
<span data-ttu-id="a4cac-179">Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4cac-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="a4cac-180">**Per assegnare gli utenti a Coupa, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="a4cac-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="a4cac-181">Nel portale di Azure classico creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="a4cac-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="a4cac-182">Nel * * Coupa * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a4cac-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="a4cac-183">![Assegnare utenti](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="a4cac-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="a4cac-184">Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="a4cac-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="a4cac-185">![Sì](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="a4cac-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="a4cac-186">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4cac-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a4cac-187">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4cac-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

