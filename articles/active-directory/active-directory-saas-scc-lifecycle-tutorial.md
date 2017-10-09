---
title: 'Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle | Microsoft Docs'
description: Informazioni su come toouse ciclo di vita SCC con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="bf29f-103">Esercitazione: Integrazione di Azure Active Directory con SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="bf29f-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="bf29f-104">obiettivo di Hello di questa esercitazione è l'integrazione di hello tooshow di Azure e ciclo di vita SCC.</span><span class="sxs-lookup"><span data-stu-id="bf29f-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="bf29f-105">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bf29f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="bf29f-106">Sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="bf29f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="bf29f-107">Sottoscrizione di SCC LifeCycle abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="bf29f-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="bf29f-108">Dopo aver completato questa esercitazione, hello Azure AD utenti assegnati tooSCC ciclo di vita sarà toosingle in grado di accesso in un'applicazione hello nel sito della società ciclo di vita SCC (accesso avviato dal provider di servizi su) o tramite hello [introduzione Pannello di accesso toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf29f-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="bf29f-109">scenario di Hello descritto in questa esercitazione è costituito da hello seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bf29f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="bf29f-110">Abilitare l'integrazione dell'applicazione hello per ciclo di vita SCC</span><span class="sxs-lookup"><span data-stu-id="bf29f-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="bf29f-111">Configurazione dell'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="bf29f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="bf29f-112">Configurazione del provisioning utente</span><span class="sxs-lookup"><span data-stu-id="bf29f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="bf29f-113">Assegnazione degli utenti</span><span class="sxs-lookup"><span data-stu-id="bf29f-113">Assigning users</span></span>

<span data-ttu-id="bf29f-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="bf29f-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="bf29f-115">Abilitare l'integrazione dell'applicazione hello per ciclo di vita SCC</span><span class="sxs-lookup"><span data-stu-id="bf29f-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="bf29f-116">obiettivo di Hello di questa sezione è toooutline come integrazione dell'applicazione hello tooenable per ciclo di vita SCC.</span><span class="sxs-lookup"><span data-stu-id="bf29f-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="bf29f-117">**integrazione dell'applicazione hello tooenable per ciclo di vita SCC, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bf29f-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf29f-118">Nel portale di Azure classico, nel riquadro di spostamento sinistro hello hello fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="bf29f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="bf29f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="bf29f-120">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="bf29f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bf29f-121">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="bf29f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="bf29f-122">![Applicazioni](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applicazioni")</span><span class="sxs-lookup"><span data-stu-id="bf29f-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="bf29f-123">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="bf29f-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="bf29f-124">![Aggiungere un'applicazione](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Aggiungere un'applicazione")</span><span class="sxs-lookup"><span data-stu-id="bf29f-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="bf29f-125">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="bf29f-126">![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")</span><span class="sxs-lookup"><span data-stu-id="bf29f-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="bf29f-127">In hello **casella di ricerca**, tipo **ciclo di vita SCC**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="bf29f-128">![Raccolta di applicazioni](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Raccolta di applicazioni")</span><span class="sxs-lookup"><span data-stu-id="bf29f-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="bf29f-129">Nel riquadro risultati hello selezionare **ciclo di vita SCC**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bf29f-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="bf29f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="bf29f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="bf29f-131">Configura accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bf29f-131">Configure single sign-on</span></span>

<span data-ttu-id="bf29f-132">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooSCC del ciclo di vita con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="bf29f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="bf29f-133">**tooconfigure accesso single sign-on, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bf29f-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf29f-134">Nel portale di Azure classico, in hello hello **ciclo di vita SCC** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** hello tooopen * * configurare Single Sign-On * * finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bf29f-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="bf29f-135">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bf29f-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="bf29f-136">In hello **come si sarebbe ad esempio utenti toosign nel ciclo di vita tooSCC** selezionare **Microsoft Azure AD Single Sign-On**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="bf29f-137">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bf29f-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="bf29f-138">In hello **Configura URL App** pagina hello **URL di accesso** casella di testo, hello digitare l'URL utilizzato dal toosign gli utenti in tooyour applicazione ciclo di vita SCC tramite hello modello "*https:// bs1.scc.com/lc7/Welcome/Customer/PICTtest.aspx*", quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="bf29f-139">![Configurare l'URL dell'app](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurare l'URL dell'app")</span><span class="sxs-lookup"><span data-stu-id="bf29f-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="bf29f-140">In hello **configurare single sign-on in ciclo di vita SCC** pagina, fare clic su **Scarica metadati**e quindi salvare il file di metadati in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="bf29f-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="bf29f-141">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bf29f-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="bf29f-142">Inoltrare tale tooSCC di file di metadati del team di supporto del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="bf29f-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="bf29f-143">Accesso Single sign-on è abilitata per il team di supporto di ciclo di vita SCC hello toobe.</span><span class="sxs-lookup"><span data-stu-id="bf29f-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="bf29f-144">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **completa** tooclose hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bf29f-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="bf29f-145">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="bf29f-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="bf29f-146">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bf29f-146">Configure user provisioning</span></span>

<span data-ttu-id="bf29f-147">In ordine tooenable Azure AD utenti toolog nel ciclo di vita SCC, è necessario eseguirne il provisioning in ciclo di vita SCC.</span><span class="sxs-lookup"><span data-stu-id="bf29f-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="bf29f-148">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooSCC del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="bf29f-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="bf29f-149">Quando toolog di tentativi di un utente assegnato nel ciclo di vita SCC, viene creato un account di ciclo di vita SCC automaticamente se necessario.</span><span class="sxs-lookup"><span data-stu-id="bf29f-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="bf29f-150">È possibile usare qualsiasi altro ciclo di vita SCC utente account strumento di creazione o qualsiasi API fornita da ciclo di vita SCC tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="bf29f-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="bf29f-151">Assegna utenti</span><span class="sxs-lookup"><span data-stu-id="bf29f-151">Assign users</span></span>
<span data-ttu-id="bf29f-152">tootest della configurazione, è necessario toogrant hello Azure AD utenti tooallow utilizzando il tooit di accesso dell'applicazione tramite l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="bf29f-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="bf29f-153">**gli utenti di tooassign tooSCC ciclo di vita, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bf29f-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf29f-154">Nel portale di Azure classico hello, creare un account di prova.</span><span class="sxs-lookup"><span data-stu-id="bf29f-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="bf29f-155">In hello * * ciclo di vita SCC * * pagina di integrazione dell'applicazione, fare clic su **assegnare gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="bf29f-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="bf29f-156">![Assegnare utenti](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="bf29f-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="bf29f-157">Selezionare l'utente test, fare clic su **assegnare**, quindi fare clic su **Sì** tooconfirm l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="bf29f-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="bf29f-158">![Sì](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sì")</span><span class="sxs-lookup"><span data-stu-id="bf29f-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="bf29f-159">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="bf29f-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="bf29f-160">Per ulteriori dettagli su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf29f-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

