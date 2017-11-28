---
title: 'Esercitazione: Integrazione di Azure Active Directory con Benefitsolver | Microsoft Docs'
description: Informazioni su come toouse Benefitsolver con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="9c888-103">Esercitazione: Integrazione di Azure Active Directory con Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="9c888-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="9c888-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="9c888-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9c888-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="9c888-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="9c888-106">A valid Azure subscription</span></span>
* <span data-ttu-id="9c888-107">Sottoscrizione di Benefitsolver abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="9c888-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9c888-108">Dopo aver completato questa esercitazione, gli utenti di hello Azure AD assegnati tooBenefitsolver saranno in grado di toosingle sign in un'applicazione hello utilizzando hello [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c888-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="9c888-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9c888-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="9c888-110">Abilitare l'integrazione dell'applicazione hello per Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="9c888-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="9c888-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="9c888-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="9c888-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="9c888-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="9c888-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="9c888-113">Assigning users</span></span>

<span data-ttu-id="9c888-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="9c888-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="9c888-115">Abilitare l'integrazione dell'applicazione hello per Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="9c888-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="9c888-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="9c888-117">integrazione dell'applicazione hello tooenable per Benefitsolver, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c888-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="9c888-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9c888-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="9c888-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="9c888-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="9c888-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="9c888-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="9c888-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="9c888-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="9c888-122">![Applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="9c888-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="9c888-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="9c888-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="9c888-124">![Aggiungere un'applicazione](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="9c888-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="9c888-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="9c888-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="9c888-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="9c888-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="9c888-127">In hello **casella di ricerca**, tipo **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="9c888-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="9c888-128">![Raccolta di applicazioni](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="9c888-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="9c888-129">Nel riquadro risultati hello selezionare **Benefitsolver**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9c888-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="9c888-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="9c888-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="9c888-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9c888-131">Configure single sign-on</span></span>

<span data-ttu-id="9c888-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooBenefitsolver con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="9c888-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="9c888-133">L'applicazione Benefitsolver prevede asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi token saml** configurazione.</span><span class="sxs-lookup"><span data-stu-id="9c888-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="9c888-134">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="9c888-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="9c888-135">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="9c888-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="9c888-136">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9c888-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="9c888-137">Nel portale di Azure classico, in hello hello **Benefitsolver** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9c888-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="9c888-138">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9c888-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="9c888-139">In hello **come si sarebbe ad esempio utenti toosign su tooBenefitsolver** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9c888-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="9c888-140">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9c888-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="9c888-141">In hello **Configura impostazioni App** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c888-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="9c888-142">![Configurare le impostazioni dell'app](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurare le impostazioni dell'app")</span><span class="sxs-lookup"><span data-stu-id="9c888-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="9c888-143">In hello **URL di accesso** casella tipo **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="9c888-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="9c888-144">In hello **URL di risposta** casella tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="9c888-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="9c888-145">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9c888-145">Click **Next**.</span></span>
4. <span data-ttu-id="9c888-146">In hello **configurare single sign-on a Benefitsolver** pagina, toodownload i metadati, fare clic su **Scarica metadati**e quindi salvare il file di metadati hello in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="9c888-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="9c888-147">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9c888-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="9c888-148">Il team di supporto Benefitsolver hello scaricato metadati file tooyour di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="9c888-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="9c888-149">Il team di supporto Benefitsolver dispone di configurazione di SSO toodo hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="9c888-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="9c888-150">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="9c888-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="9c888-151">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9c888-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="9c888-152">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="9c888-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="9c888-153">Scegliere dal menu hello in primo piano hello **attributi** tooopen hello **attributi Token SAML** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9c888-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="9c888-154">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="9c888-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="9c888-155">mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c888-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="9c888-156">![Attributi](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="9c888-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="9c888-157">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="9c888-157">Attribute Name</span></span> | <span data-ttu-id="9c888-158">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="9c888-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="9c888-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="9c888-159">ClientID</span></span> |<span data-ttu-id="9c888-160">È necessario tooget questo valore dal team di supporto Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="9c888-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="9c888-161">ClientKey</span></span> |<span data-ttu-id="9c888-162">È necessario tooget questo valore dal team di supporto Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="9c888-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="9c888-163">LogoutURL</span></span> |<span data-ttu-id="9c888-164">È necessario tooget questo valore dal team di supporto Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="9c888-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="9c888-165">EmployeeID</span></span> |<span data-ttu-id="9c888-166">È necessario tooget questo valore dal team di supporto Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="9c888-167">Per ogni riga di dati della tabella hello precedente, fare clic su **Aggiungi attributo utente**.</span><span class="sxs-lookup"><span data-stu-id="9c888-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="9c888-168">In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="9c888-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="9c888-169">In hello **valore dell'attributo** casella di testo, il valore di attributo hello selezionare mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="9c888-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="9c888-170">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9c888-170">Click **Complete**.</span></span>
9. <span data-ttu-id="9c888-171">Fare clic su **Applica modifiche**.</span><span class="sxs-lookup"><span data-stu-id="9c888-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="9c888-172">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="9c888-172">Configure user provisioning</span></span>
<span data-ttu-id="9c888-173">In ordine tooenable Azure AD utenti toolog in Benefitsolver, è necessario eseguirne il provisioning in Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="9c888-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="9c888-174">Nel caso di hello di Benefitsolver, i dati dei dipendenti sono nell'applicazione compilata tramite un file di censimento dal sistema HRIS (in genere durante la notte).</span><span class="sxs-lookup"><span data-stu-id="9c888-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="9c888-175">È possibile usare qualsiasi altro Benefitsolver utente account strumento di creazione o le API fornite da Benefitsolver tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="9c888-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="9c888-176">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="9c888-176">Assigning users</span></span>
<span data-ttu-id="9c888-177">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="9c888-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="9c888-178">tooassign tooBenefitsolver di utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9c888-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="9c888-179">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="9c888-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="9c888-180">In hello * * Benefitsolver * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9c888-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="9c888-181">![Assegnare utenti](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="9c888-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="9c888-182">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="9c888-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="9c888-183">![Sì](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="9c888-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="9c888-184">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="9c888-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="9c888-185">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c888-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

