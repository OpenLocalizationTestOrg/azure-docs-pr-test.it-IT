---
title: aaaConfigure eseguire come Account di Azure | Documenti Microsoft
description: "In questa esercitazione viene tramite l'utilizzo di creazione, test e l'esempio hello di autenticazione di entità di sicurezza in automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nome entità servizio, setspn, autenticazione di Azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="dd7aa-104">Autenticare runbook con un account RunAs di Azure</span><span class="sxs-lookup"><span data-stu-id="dd7aa-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="dd7aa-105">In questo articolo viene illustrato come l'account tooconfigure un'automazione di Azure hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="dd7aa-106">toodo in tal caso, utilizzare hello Run As account funzionalità tooauthenticate runbook di gestione delle risorse di Azure Resource Manager o Gestione servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="dd7aa-107">Quando si crea un account di automazione in hello portale di Azure, viene creata automaticamente due account:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="dd7aa-108">Un account RunAs.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-108">A Run As account.</span></span> <span data-ttu-id="dd7aa-109">Questo account crea un'entità servizio in Azure Active Directory (Azure AD) e un certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="dd7aa-110">Assegna inoltre hello collaboratore basata sui ruoli access control (RBAC), che gestisce le risorse di gestione delle risorse con i runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="dd7aa-111">Un account RunAs classico.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-111">A Classic Run As account.</span></span> <span data-ttu-id="dd7aa-112">Questo account consente di caricare un certificato di gestione, viene utilizzato toomanage gestione dei servizi o le risorse classiche utilizzando runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="dd7aa-113">Creazione di un account semplifica il processo di hello per l'utente e consente di che iniziare rapidamente la creazione e distribuzione toosupport runbook di automazione dell'automazione è necessario.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="dd7aa-114">Con un account RunAs e un account RunAs classico è possibile:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="dd7aa-115">Fornire un modo standardizzato di tooauthenticate Azure quando si gestiscono Gestione risorse o le risorse di gestione dei servizi da runbook nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="dd7aa-116">Automatizzare l'uso di hello dei runbook globale, che è possibile configurare avvisi di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7aa-117">Hello [funzionalità di integrazione di Azure avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) con l'automazione runbook globale richiede un account di automazione che è configurato con un account RunAs e un classico account RunAs.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="dd7aa-118">È possibile selezionare un account di automazione già definito account RunAs e classico runas oppure è possibile scegliere un nuovo account di automazione toocreate.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="dd7aa-119">Questo articolo illustra come toocreate un account di automazione da hello portale di Azure, aggiornare un account di automazione usando Azure PowerShell, gestire la configurazione di account hello e l'autenticazione dei runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="dd7aa-120">Prima di iniziare la creazione di un account di automazione, è una buona idea toounderstand e considerare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="dd7aa-121">Creazione di un account di automazione non influenza gli account di automazione che è potrebbe essere già stato creato in hello classic o il modello di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="dd7aa-122">il processo di Hello funziona solo per gli account di automazione creati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="dd7aa-123">Il tentativo di un account dal portale di Azure classico hello toocreate, configurazione runas hello dell'account non viene replicato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="dd7aa-124">Se si dispone già runbook e risorse, quali le pianificazioni o variabili, le risorse classiche di toomanage sul posto, e si desidera tooauthenticate runbook con hello nuovo classico account RunAs, eseguire una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="dd7aa-125">toocreate un classico account RunAs, seguire le istruzioni di hello nella sezione "Gestire l'account Esegui come" hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="dd7aa-126">tooupdate account esistente, utilizzare hello PowerShell script nella sezione "Aggiornare l'account di automazione usando PowerShell" hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="dd7aa-127">tooauthenticate utilizzando hello nuovo account RunAs e classico eseguire come account di automazione di, è necessario che i runbook esistenti con il codice di esempio fornito nella sezione hello di hello toomodify [esempi di codice di autenticazione](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="dd7aa-128">account RunAs Hello è per l'autenticazione rispetto alle risorse di gestione risorse usando hello entità di servizio basata su certificati.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="dd7aa-129">Hello Classic account RunAs è per l'autenticazione nel servizio Gestione risorse con un certificato di gestione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="dd7aa-130">Creare un account di automazione da hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd7aa-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="dd7aa-131">In questa sezione creare un account di automazione di Azure dal portale di Azure, che a sua volta crea un account RunAs sia un classico account RunAs hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="dd7aa-132">toocreate un account di automazione, è necessario essere un membro del ruolo Amministratori servizio hello o coamministratori della sottoscrizione hello che concede l'accesso toohello sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="dd7aa-133">È inoltre necessario essere aggiunto come istanza di Active Directory della sottoscrizione di toothat utente predefinito.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="dd7aa-134">account Hello non è necessario toobe assegnato un ruolo con privilegi.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="dd7aa-135">Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di ruoli di toohello CO-amministratore della sottoscrizione di hello, verranno aggiunti tooActive Directory come guest.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="dd7aa-136">In questo caso, si riceverà un "non si dispone delle autorizzazioni toocreate..."</span><span class="sxs-lookup"><span data-stu-id="dd7aa-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="dd7aa-137">visualizzazione dell'avviso hello **aggiungere Account di automazione** blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="dd7aa-138">Gli utenti che sono stati aggiunti al ruolo di CO-amministratore toohello innanzitutto può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake loro un utente in Active Directory completa.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="dd7aa-139">tooverify tale situazione hello **Azure Active Directory** riquadro nel portale di Azure selezionando hello **utenti e gruppi**, se si seleziona **tutti gli utenti** e, dopo aver selezionato utente specifico di Hello, selezionando **profilo**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="dd7aa-140">valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="dd7aa-141">Accedi a portale di Azure con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello toohello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="dd7aa-142">Selezionare **Account di automazione**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="dd7aa-143">In hello **gli account di automazione** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="dd7aa-144">Hello **aggiungere Account di automazione** apre blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-144">hello **Add Automation Account** blade opens.</span></span>

 ![pannello "Aggiungi Account di automazione" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="dd7aa-146">Se l'account non è un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione di hello, hello seguente avviso è visualizzato nella hello **aggiungere Account di automazione** pannello:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Aggiungi account di Automazione, avviso](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="dd7aa-148">In hello **aggiungere Account di automazione** pannello in hello **nome** , digitare un nome per il nuovo account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="dd7aa-149">Se si dispone di più di una sottoscrizione, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="dd7aa-150">a.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-150">a.</span></span> <span data-ttu-id="dd7aa-151">In **sottoscrizione**, specificare un nuovo account hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="dd7aa-152">b.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-152">b.</span></span> <span data-ttu-id="dd7aa-153">In **Gruppo di risorse** fare clic su **Crea nuovo** o **Usa esistente**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="dd7aa-154">c.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-154">c.</span></span> <span data-ttu-id="dd7aa-155">In **Località** specificare un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="dd7aa-156">In **Crea un account RunAs di Azure** scegliere **Sì** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd7aa-157">Se si sceglie di non toocreate hello account RunAs selezionando **n**, viene visualizzato un messaggio di avviso hello **aggiungere Account di automazione** blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="dd7aa-158">Nonostante hello account viene creato nel portale di Azure hello, non presenta un'identità di autenticazione corrispondente all'interno del classica o servizio directory di gestione risorse di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="dd7aa-159">Di conseguenza, hello non disponga di alcun tooresources accesso nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="dd7aa-160">Questo scenario impedisce ai runbook che fanno riferimento a questo account di autenticarsi ed eseguire attività sulle risorse in tali modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Messaggio di avviso nel Pannello di "Aggiungere Account di automazione" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="dd7aa-162">Inoltre, poiché non viene creata un'entità servizio hello, ruolo di collaboratore hello non è assegnato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="dd7aa-163">Mentre Azure crea account di automazione hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="dd7aa-164">Risorse</span><span class="sxs-lookup"><span data-stu-id="dd7aa-164">Resources</span></span>
<span data-ttu-id="dd7aa-165">Quando viene creato correttamente hello account di automazione, varie risorse vengono create automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="dd7aa-166">risorse Hello sono riepilogate nella hello le due tabelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="dd7aa-167">Risorse dell'account RunAs</span><span class="sxs-lookup"><span data-stu-id="dd7aa-167">Run As account resources</span></span>

| <span data-ttu-id="dd7aa-168">Risorsa</span><span class="sxs-lookup"><span data-stu-id="dd7aa-168">Resource</span></span> | <span data-ttu-id="dd7aa-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd7aa-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd7aa-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="dd7aa-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="dd7aa-171">Un runbook grafico di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="dd7aa-172">Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="dd7aa-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="dd7aa-173">Un runbook di PowerShell di esempio che illustra come tooauthenticate utilizzando hello account RunAs e recupera tutte le risorse di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="dd7aa-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="dd7aa-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="dd7aa-175">asset del certificato Hello che viene creato automaticamente quando si crea un account di automazione o utilizza hello seguente script di PowerShell per un account esistente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="dd7aa-176">certificato Hello consente tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure Resource Manager dai runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="dd7aa-177">certificato Hello ha una durata di un anno.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="dd7aa-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="dd7aa-178">AzureRunAsConnection</span></span> | <span data-ttu-id="dd7aa-179">asset della connessione Hello che viene creato automaticamente quando si crea un account di automazione o utilizza uno script di PowerShell hello per un account esistente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="dd7aa-180">Risorse dell'account RunAs classico</span><span class="sxs-lookup"><span data-stu-id="dd7aa-180">Classic Run As account resources</span></span>

| <span data-ttu-id="dd7aa-181">Risorsa</span><span class="sxs-lookup"><span data-stu-id="dd7aa-181">Resource</span></span> | <span data-ttu-id="dd7aa-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd7aa-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd7aa-183">Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="dd7aa-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="dd7aa-184">Un runbook grafico di esempio che ottiene tutte le macchine virtuali hello che vengono creati usando il modello di distribuzione classica hello in una sottoscrizione con hello Classic account RunAs (certificato) e quindi scrive lo stato e nome della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="dd7aa-185">Runbook di script AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="dd7aa-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="dd7aa-186">Un runbook di PowerShell di esempio che ottiene tutti hello delle macchine virtuali classiche in una sottoscrizione utilizzando hello Classic account RunAs (certificato) e quindi scrive hello lo stato e nome della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="dd7aa-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="dd7aa-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="dd7aa-188">asset del certificato creato automaticamente Hello usare tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="dd7aa-189">certificato Hello ha una durata di un anno.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="dd7aa-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="dd7aa-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="dd7aa-191">asset di connessione creati automaticamente Hello usare tooauthenticate con Azure in modo che è possibile gestire le risorse di Azure classiche dai runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="dd7aa-192">Verificare l'autenticazione con RunAs</span><span class="sxs-lookup"><span data-stu-id="dd7aa-192">Verify Run As authentication</span></span>
<span data-ttu-id="dd7aa-193">Eseguire un test di piccole dimensioni di tooconfirm che può eseguire l'autenticazione tramite hello nuovo account RunAs.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="dd7aa-194">Nel portale di Azure hello, aprire l'account di automazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="dd7aa-195">Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="dd7aa-196">Seleziona hello **AzureAutomationTutorialScript** runbook, quindi fare clic su **avviare** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="dd7aa-197">si verifica Hello seguenti eventi:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-197">hello following events occur:</span></span>
 * <span data-ttu-id="dd7aa-198">Oggetto [processo del runbook](automation-runbook-execution.md) viene creato, hello **processo** blade viene visualizzata e viene visualizzato lo stato del processo hello in hello **riepilogo** riquadro.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="dd7aa-199">lo stato del processo Hello inizia come **in coda**, che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="dd7aa-200">stato Hello diventa **iniziale** quando un thread di lavoro attestazioni processo hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="dd7aa-201">stato Hello diventa **esecuzione** quando runbook hello viene avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="dd7aa-202">Completamento dell'esecuzione di processo del runbook hello, verrà visualizzato lo stato **completato**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="dd7aa-203">toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="dd7aa-204">Hello **Output** pannello è visualizzato, contenente runbook hello autenticato e ha restituito un elenco di tutte le risorse disponibili nel gruppo di risorse hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="dd7aa-205">Chiude hello **Output** pannello tooreturn toohello **riepilogo** blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="dd7aa-206">Chiude hello **riepilogo** blade e hello corrispondente **AzureAutomationTutorialScript** pannello runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="dd7aa-207">Verificare l'autenticazione con RunAs classico</span><span class="sxs-lookup"><span data-stu-id="dd7aa-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="dd7aa-208">Eseguire una piccola simile test tooconfirm che può eseguire l'autenticazione tramite hello nuovo classico account RunAs.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="dd7aa-209">Nel portale di Azure hello, aprire l'account di automazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="dd7aa-210">Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="dd7aa-211">Seleziona hello **AzureClassicAutomationTutorialScript** runbook, quindi fare clic su **avviare** troppo avviare runbook hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="dd7aa-212">si verifica Hello seguenti eventi:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-212">hello following events occur:</span></span>

 * <span data-ttu-id="dd7aa-213">Oggetto [processo del runbook](automation-runbook-execution.md) viene creato, hello **processo** blade viene visualizzata e viene visualizzato lo stato del processo hello in hello **riepilogo** riquadro.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="dd7aa-214">lo stato del processo Hello inizia come **in coda**, che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="dd7aa-215">stato Hello diventa **iniziale** quando un thread di lavoro attestazioni processo hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="dd7aa-216">stato Hello diventa **esecuzione** quando runbook hello viene avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="dd7aa-217">Completamento dell'esecuzione di processo del runbook hello, verrà visualizzato lo stato **completato**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Verifica del runbook dell'entità di sicurezza](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="dd7aa-219">toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="dd7aa-220">Hello **Output** pannello è visualizzato, contenente runbook hello autenticato e ha restituito un elenco di tutte le macchine virtuali classiche nella sottoscrizione hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="dd7aa-221">Chiude hello **Output** pannello tooreturn toohello **riepilogo** blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="dd7aa-222">Chiude hello **riepilogo** blade e hello corrispondente **AzureAutomationTutorialScript** pannello runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="dd7aa-223">Gestire l'account RunAs</span><span class="sxs-lookup"><span data-stu-id="dd7aa-223">Managing your Run As account</span></span>
<span data-ttu-id="dd7aa-224">A un certo punto prima che scada l'account di automazione, sarà necessario toorenew hello certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="dd7aa-225">Se si ritiene che hello account RunAs sia stata compromessa, è possibile eliminare e ricrearlo.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="dd7aa-226">Questa sezione viene descritto come tooperform queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="dd7aa-227">Rinnovo del certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="dd7aa-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="dd7aa-228">il certificato autofirmato Hello creato per l'account RunAs hello scade un anno dalla data di hello di creazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="dd7aa-229">È possibile rinnovarlo in qualsiasi momento prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="dd7aa-230">Quando si rinnovarlo, certificato valido corrente hello è conservate tooensure che tutti i runbook che vengono messe in coda fino o attivamente in esecuzione e che l'autenticazione con hello account RunAs, non sono influenzati negativamente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="dd7aa-231">certificato Hello rimane valido fino alla relativa data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7aa-232">Se si utilizza questa opzione è stata configurata l'automazione Run As account toouse un certificato emesso da un'autorità di certificazione dell'organizzazione, certificato aziendale hello verrà sostituito da un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="dd7aa-233">hello toorenew certificati, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="dd7aa-234">Nel portale di Azure hello, aprire l'account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="dd7aa-235">In hello **Account di automazione** pannello in hello **Account proprietà** riquadro, in **impostazioni Account**selezionare **account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Riquadro delle proprietà dell'account di Automazione](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="dd7aa-237">In hello **account RunAs** Pannello proprietà, seleziona entrambi hello eseguiti come account o hello Classic account RunAs che si desidera che il certificato hello toorenew per.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="dd7aa-238">In hello **proprietà** pannello hello account selezionato, fare clic su **Rinnova certificato**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Rinnovare il certificato per l'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="dd7aa-240">Mentre viene rinnovato il certificato di hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="dd7aa-241">Eliminare un account RunAs o un account RunAs classico</span><span class="sxs-lookup"><span data-stu-id="dd7aa-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="dd7aa-242">Questa sezione viene descritto come toodelete e ricreare un account RunAs o classico runas.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="dd7aa-243">Quando si esegue questa azione, viene mantenuto hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="dd7aa-244">Dopo aver eliminato un account RunAs o classico runas, è possibile crearlo nuovamente in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="dd7aa-245">Nel portale di Azure hello, aprire l'account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="dd7aa-246">In hello **account di automazione** in hello account riquadro proprietà, seleziona pannello **account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="dd7aa-247">In hello **account RunAs** Pannello proprietà, selezionare entrambi hello account RunAs classico RunAs dell'account che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="dd7aa-248">Quindi, nella hello **proprietà** pannello hello account selezionato, fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Eliminare un account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="dd7aa-250">Durante l'eliminazione di account hello in corso, è possibile monitorare i progressi di hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="dd7aa-251">Dopo aver eliminato l'account di hello, è possibile crearlo nuovamente su hello **account RunAs** Pannello proprietà selezionando hello opzione create **Azure Account runas**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Ricreare hello automazione account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="dd7aa-253">Errore di configurazione</span><span class="sxs-lookup"><span data-stu-id="dd7aa-253">Misconfiguration</span></span>
<span data-ttu-id="dd7aa-254">Alcuni elementi di configurazione necessari per toofunction di account RunAs o classico runas hello correttamente potrebbe essere stati eliminati o creati in modo non corretto durante l'installazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="dd7aa-255">gli elementi di Hello includono:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-255">hello items include:</span></span>

* <span data-ttu-id="dd7aa-256">Asset del certificato</span><span class="sxs-lookup"><span data-stu-id="dd7aa-256">Certificate asset</span></span>
* <span data-ttu-id="dd7aa-257">Asset di connessione</span><span class="sxs-lookup"><span data-stu-id="dd7aa-257">Connection asset</span></span>
* <span data-ttu-id="dd7aa-258">Account RunAs è stato rimosso dal ruolo di collaboratore hello</span><span class="sxs-lookup"><span data-stu-id="dd7aa-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="dd7aa-259">Entità servizio o applicazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7aa-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="dd7aa-260">In altre istanze di una configurazione errata e hello precedente hello account di automazione rileva hello cambia e visualizza lo stato di *incompleto* su hello **account RunAs** Pannello proprietà per hello account.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Stato di configurazione Incompleto dell'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="dd7aa-262">Quando si seleziona account RunAs hello, hello account **proprietà** riquadro Visualizza hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Messaggio di avviso relativo alla configurazione incompleta dell'account RunAs](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="dd7aa-264">.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-264">.</span></span>

<span data-ttu-id="dd7aa-265">Per risolvere rapidamente i problemi di account RunAs, eliminazione e ricreazione account hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="dd7aa-266">Aggiornare l'account di Automazione usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd7aa-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="dd7aa-267">È possibile utilizzare l'account di automazione esistente PowerShell tooupdate se:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="dd7aa-268">Si crea un account di automazione, ma rifiuta toocreate account RunAs hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="dd7aa-269">Già in uso un risorse di gestione risorse di automazione account toomanage e si desidera tooupdate hello account tooinclude hello account RunAs per l'autenticazione di runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="dd7aa-270">Già in uso un'automazione account toomanage classico alle risorse e si desidera tooupdate è toouse hello Classic account RunAs anziché creare un nuovo account e la migrazione tooit i runbook e le risorse.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="dd7aa-271">Si desidera toocreate Esegui come e un classico account RunAs utilizzando un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="dd7aa-272">script Hello è hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="dd7aa-273">script di Hello può essere eseguito solo in Windows 10 e Windows Server 2016 con moduli di gestione risorse di Azure 2.01 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="dd7aa-274">Non sono supportate le versioni precedenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="dd7aa-275">Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="dd7aa-276">Per informazioni sulla versione di hello PowerShell 1.0, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="dd7aa-277">Un account di automazione cui viene fatto riferimento come valore hello hello *– AutomationAccountName* e *- ApplicationDisplayName* parametri hello lo script di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="dd7aa-278">i valori hello tooget per *SubscriptionID*, *gruppo di risorse*, e *AutomationAccountName*, che sono parametri obbligatori per gli script hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="dd7aa-279">In hello portale di Azure, selezionare l'account di automazione in hello **account di automazione** blade e quindi selezionare **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="dd7aa-280">In hello **tutte le impostazioni** pannello, in **impostazioni Account**selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="dd7aa-281">Notare i valori hello in hello **proprietà** blade.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-281">Note hello values on hello **Properties** blade.</span></span>

![Pannello di "Proprietà" Hello automazione account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="dd7aa-283">Creare lo script di PowerShell per l'account RunAs</span><span class="sxs-lookup"><span data-stu-id="dd7aa-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="dd7aa-284">Questo script di PowerShell include il supporto per hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="dd7aa-285">Creare un account RunAs usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="dd7aa-286">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="dd7aa-287">Creare un account RunAs e un account RunAs classico usando un certificato enterprise.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="dd7aa-288">Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="dd7aa-289">A seconda opzione di configurazione hello selezionata, lo script di hello crea hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="dd7aa-290">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="dd7aa-291">Crea un Azure AD applicazione toobe esportato con entrambi hello autofirmato o chiave pubblica del certificato dell'organizzazione, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna hello ruolo Collaboratore per conto di hello in corrente sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="dd7aa-292">È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="dd7aa-293">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="dd7aa-294">Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="dd7aa-295">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="dd7aa-296">Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="dd7aa-297">asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="dd7aa-298">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="dd7aa-299">Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="dd7aa-300">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="dd7aa-301">Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="dd7aa-302">asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="dd7aa-303">Se si seleziona l'opzione desiderata per la creazione di un classico account RunAs, dopo l'esecuzione di script hello, caricamento hello pubblica Gestione toohello (estensione del nome file con estensione cer) dell'archivio certificati per la sottoscrizione di hello che hello account di automazione è stato creato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="dd7aa-304">tooexecute hello script e caricare il certificato di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="dd7aa-305">Salvare lo script seguente nel computer in uso hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-305">Save hello following script on your computer.</span></span> <span data-ttu-id="dd7aa-306">In questo esempio, salvarlo con il nome file hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="dd7aa-307">Fare clic sul menu **Start** del computer e avviare **Windows PowerShell** con diritti utente elevati.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="dd7aa-308">Da hello elevati shell della riga di comando di PowerShell, passare toohello cartella che contiene lo script hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="dd7aa-309">Eseguire script hello utilizzando i valori dei parametri hello per la configurazione di hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="dd7aa-310">**Creare un account RunAs usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="dd7aa-311">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="dd7aa-312">**Creare un account RunAs e un account RunAs classico usando un certificato enterprise**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="dd7aa-313">**Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici**</span><span class="sxs-lookup"><span data-stu-id="dd7aa-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="dd7aa-314">Dopo l'esecuzione di script hello è, sarà richiesta tooauthenticate con Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="dd7aa-315">Accedere con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="dd7aa-316">Dopo l'esecuzione dello script hello completata, si noti seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="dd7aa-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="dd7aa-317">Se è stato creato un classico account RunAs con un certificato pubblico autofirmato (file con estensione cer), script hello crea e Salva toohello cartella dei file temporanei nel computer in uso nel profilo utente hello *%USERPROFILE%\AppData\Local\Temp*, sessione di PowerShell hello tooexecute utilizzati.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="dd7aa-318">Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="dd7aa-319">Seguire le istruzioni di hello per [caricando un toohello certificato API di Gestione portale di Azure classico](../azure-api-management-certs.md)e convalidare una configurazione di hello delle credenziali con risorse di gestione dei servizi tramite hello [codice di esempio tooauthenticate con servizio di gestione delle risorse](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="dd7aa-320">Se è stato eseguito *non* creare un classico account RunAs, l'autenticazione con le risorse di gestione delle risorse e convalidare la configurazione di credenziali di hello utilizzando hello [codice per l'autenticazione con gestione del servizio di esempio risorse](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="dd7aa-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="dd7aa-321">Tooauthenticate codice di esempio con le risorse di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="dd7aa-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="dd7aa-322">È possibile utilizzare il seguente hello aggiornato codice di esempio, prelevato hello *AzureAutomationTutorialScript* runbook di esempio, tooauthenticate utilizzando hello Run As account toomanage Gestione risorse alle risorse con i runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="dd7aa-323">toohelp è tooeasily funziona tra più sottoscrizioni, script hello include due ulteriori righe di codice che supportano che fanno riferimento a un contesto di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="dd7aa-324">Un asset della variabile denominato *SubscriptionId* contiene hello ID di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="dd7aa-325">Dopo aver hello `Add-AzureRmAccount` cmdlet istruzione hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet viene dichiarata con il set di parametri di hello *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="dd7aa-326">Se il nome di variabile hello è troppo generico, è possibile correggerlo tooinclude un prefisso o utilizzare un altro toomake convenzione denominazione si tooidentify più semplice.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="dd7aa-327">In alternativa, è possibile utilizzare il set di parametri di hello *- SubscriptionName* anziché *- SubscriptionId* con un asset della variabile corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="dd7aa-328">i cmdlet utilizzati per l'autenticazione in runbook hello, Hello `Add-AzureRmAccount`, hello utilizza *ServicePrincipalCertificate* set di parametri.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="dd7aa-329">Consente l'autenticazione tramite certificato principale hello del servizio, non le credenziali utente hello.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="dd7aa-330">Tooauthenticate codice di esempio con le risorse di gestione dei servizi</span><span class="sxs-lookup"><span data-stu-id="dd7aa-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="dd7aa-331">È possibile utilizzare hello seguente codice di esempio aggiornato, che viene utilizzato da hello *AzureClassicAutomationTutorialScript* runbook di esempio, tooauthenticate utilizzando hello Classic account RunAs toomanage le risorse classiche con il runbook.</span><span class="sxs-lookup"><span data-stu-id="dd7aa-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="dd7aa-332">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd7aa-332">Next steps</span></span>
* [<span data-ttu-id="dd7aa-333">Oggetti applicazione e oggetti entità servizio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd7aa-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="dd7aa-334">Controllo degli accessi in base al ruolo in Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dd7aa-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="dd7aa-335">Panoramica sui certificati per i servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="dd7aa-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
