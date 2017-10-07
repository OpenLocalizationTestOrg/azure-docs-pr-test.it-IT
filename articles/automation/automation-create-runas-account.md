---
title: account di automazione runas di Azure aaaCreate | Documenti Microsoft
description: Questo articolo viene descritto come tooupdate l'automazione dell'account e creare gli account RunAs con PowerShell o dal portale di hello.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="367b3-103">Aggiornare l'autenticazione dell'account di Automazione con account RunAs</span><span class="sxs-lookup"><span data-stu-id="367b3-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="367b3-104">È possibile aggiornare l'account di automazione esistente dal portale hello o se l'utilizzo di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="367b3-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="367b3-105">Si crea un account di automazione, ma rifiuta toocreate account RunAs hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="367b3-106">Già in uso un risorse di gestione risorse di automazione account toomanage e si desidera tooupdate hello account tooinclude hello account RunAs per l'autenticazione di runbook.</span><span class="sxs-lookup"><span data-stu-id="367b3-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="367b3-107">Già in uso un'automazione account toomanage classico alle risorse e si desidera tooupdate è toouse hello Classic account RunAs anziché creare un nuovo account e la migrazione tooit i runbook e le risorse.</span><span class="sxs-lookup"><span data-stu-id="367b3-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="367b3-108">Si desidera toocreate Esegui come e un classico account RunAs utilizzando un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA).</span><span class="sxs-lookup"><span data-stu-id="367b3-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="367b3-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="367b3-109">Prerequisites</span></span>

* <span data-ttu-id="367b3-110">Hello script può essere eseguito solo in Windows 10 e Windows Server 2016 con moduli di gestione risorse di Azure 3.0.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="367b3-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="367b3-111">Non sono supportate le versioni precedenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="367b3-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="367b3-112">Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="367b3-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="367b3-113">Per informazioni sulla versione di hello PowerShell 1.0, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="367b3-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="367b3-114">Un account di automazione cui viene fatto riferimento come valore hello hello *– AutomationAccountName* e *- ApplicationDisplayName* parametri hello lo script di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="367b3-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="367b3-115">i valori hello tooget per *SubscriptionID*, *gruppo di risorse*, e *AutomationAccountName*, che sono parametri obbligatori per lo script hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="367b3-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="367b3-116">In hello portale di Azure, selezionare l'account di automazione in hello **account di automazione** blade e quindi selezionare **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="367b3-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="367b3-117">In hello **tutte le impostazioni** pannello, in **impostazioni Account**selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="367b3-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="367b3-118">Notare i valori hello in hello **proprietà** blade.</span><span class="sxs-lookup"><span data-stu-id="367b3-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="367b3-119">![Pannello di "Proprietà" Hello automazione account](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="367b3-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="367b3-120">Necessarie autorizzazioni tooupdate l'account di automazione</span><span class="sxs-lookup"><span data-stu-id="367b3-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="367b3-121">tooupdate un account di automazione, è necessario disporre di privilegi specifici seguenti hello e le autorizzazioni necessarie toocomplete in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="367b3-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="367b3-122">L'account utente di Active Directory deve toobe tooa aggiunto ruolo con ruolo di collaboratore toohello equivalenti autorizzazioni per le risorse di Microsoft, come illustrato nell'articolo [controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="367b3-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="367b3-123">Gli utenti senza privilegi di amministratore nel tenant di Azure AD possono [registrare applicazioni AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se registrazioni di App hello impostazione è troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="367b3-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="367b3-124">Se le registrazioni di app hello impostazione è troppo**n**, utente hello eseguendo questa azione deve essere un amministratore globale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="367b3-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="367b3-125">Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di toohello amministratore/coamministratore ruolo globale della sottoscrizione di hello, tooActive Directory aggiunti come guest.</span><span class="sxs-lookup"><span data-stu-id="367b3-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="367b3-126">In questo caso, viene visualizzato un "non si dispone delle autorizzazioni toocreate..."</span><span class="sxs-lookup"><span data-stu-id="367b3-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="367b3-127">visualizzazione dell'avviso hello **aggiungere Account di automazione** blade.</span><span class="sxs-lookup"><span data-stu-id="367b3-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="367b3-128">Gli utenti che sono stati aggiunti toohello amministratore/coamministratore ruolo globale può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake prima li un utente in Active Directory completa.</span><span class="sxs-lookup"><span data-stu-id="367b3-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="367b3-129">tooverify tale situazione, hello **Azure Active Directory** riquadro nel portale di Azure selezionare hello **utenti e gruppi**selezionare **tutti gli utenti** e, dopo aver selezionato hello un utente specifico, seleziona **profilo**.</span><span class="sxs-lookup"><span data-stu-id="367b3-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="367b3-130">valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.</span><span class="sxs-lookup"><span data-stu-id="367b3-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="367b3-131">Creare account RunAs dal portale hello</span><span class="sxs-lookup"><span data-stu-id="367b3-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="367b3-132">In questa sezione, eseguire hello seguendo i passaggi tooupdate l'account di automazione di Azure dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="367b3-133">Creerai hello account RunAs e classico runas singolarmente, e se non sono necessarie risorse toomanage nel portale di Azure classico hello, è possibile creare hello Azure account RunAs.</span><span class="sxs-lookup"><span data-stu-id="367b3-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="367b3-134">il processo di Hello crea hello elementi nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="367b3-135">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="367b3-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="367b3-136">Crea un'applicazione Azure AD con un certificato autofirmato, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna il ruolo di collaboratore hello per conto di hello nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="367b3-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="367b3-137">È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="367b3-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="367b3-138">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="367b3-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="367b3-139">Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-140">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="367b3-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="367b3-141">Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-142">asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="367b3-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="367b3-143">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="367b3-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="367b3-144">Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-145">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="367b3-146">Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-147">asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.</span><span class="sxs-lookup"><span data-stu-id="367b3-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="367b3-148">Accedi toohello portale di Azure con un account che sia un membro del ruolo di amministratori della sottoscrizione hello e al coamministratore della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="367b3-149">Dal Pannello di account di automazione hello, selezionare **account RunAs** nella sezione hello **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="367b3-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="367b3-150">A seconda del tipo di account necessario, selezionare **Account RunAs di Azure** o **Account RunAs classico di Azure**.</span><span class="sxs-lookup"><span data-stu-id="367b3-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="367b3-151">Dopo aver selezionato uno hello **aggiungere Azure runas** o **aggiungere Azure classico Account runas** pannello viene visualizzato e dopo aver esaminato le informazioni generali di hello, fare clic su **crea** tooproceed con la creazione di account RunAs.</span><span class="sxs-lookup"><span data-stu-id="367b3-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="367b3-152">Mentre Azure crea account RunAs hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** da hello menu e un messaggio viene visualizzato indicante account hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="367b3-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="367b3-153">Questo processo può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="367b3-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="367b3-154">Creare un account RunAs usando lo script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="367b3-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="367b3-155">Questo script di PowerShell include il supporto per hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="367b3-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="367b3-156">Creare un account RunAs usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="367b3-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="367b3-157">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="367b3-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="367b3-158">Creare un account RunAs e un account RunAs classico usando un certificato enterprise.</span><span class="sxs-lookup"><span data-stu-id="367b3-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="367b3-159">Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="367b3-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="367b3-160">A seconda opzione di configurazione hello selezionata, lo script di hello crea hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="367b3-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="367b3-161">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="367b3-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="367b3-162">Crea un Azure AD applicazione toobe esportato con entrambi hello autofirmato o chiave pubblica del certificato dell'organizzazione, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna hello ruolo Collaboratore per conto di hello in corrente sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="367b3-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="367b3-163">È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="367b3-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="367b3-164">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="367b3-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="367b3-165">Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-166">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="367b3-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="367b3-167">Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-168">asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="367b3-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="367b3-169">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="367b3-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="367b3-170">Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-171">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="367b3-172">Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="367b3-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="367b3-173">asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.</span><span class="sxs-lookup"><span data-stu-id="367b3-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="367b3-174">Se si seleziona l'opzione desiderata per la creazione di un classico account RunAs, dopo l'esecuzione di script hello, caricamento hello pubblica Gestione toohello (estensione del nome file con estensione cer) dell'archivio certificati per la sottoscrizione di hello che hello account di automazione è stato creato.</span><span class="sxs-lookup"><span data-stu-id="367b3-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="367b3-175">Salvare lo script seguente nel computer in uso hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-175">Save hello following script on your computer.</span></span> <span data-ttu-id="367b3-176">In questo esempio, salvarlo con il nome file hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="367b3-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="367b3-177">Nel computer, avviare **Windows PowerShell** da hello **avviare** schermata con diritti utente elevati.</span><span class="sxs-lookup"><span data-stu-id="367b3-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="367b3-178">Da hello elevati shell della riga di comando, passare toohello cartella che contiene lo script hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="367b3-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="367b3-179">Eseguire script hello utilizzando i valori dei parametri hello per la configurazione di hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="367b3-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="367b3-180">**Creare un account RunAs usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="367b3-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="367b3-181">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="367b3-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="367b3-182">**Creare un account RunAs e un account RunAs classico usando un certificato enterprise**</span><span class="sxs-lookup"><span data-stu-id="367b3-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="367b3-183">**Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici**</span><span class="sxs-lookup"><span data-stu-id="367b3-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="367b3-184">Dopo l'esecuzione di script hello è, sarà richiesta tooauthenticate con Azure.</span><span class="sxs-lookup"><span data-stu-id="367b3-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="367b3-185">Accedere con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="367b3-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="367b3-186">Dopo l'esecuzione dello script hello completata, si noti seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="367b3-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="367b3-187">Se è stato creato un classico account RunAs con un certificato pubblico autofirmato (file con estensione cer), script hello crea e Salva toohello cartella dei file temporanei nel computer in uso nel profilo utente hello *%USERPROFILE%\AppData\Local\Temp*, sessione di PowerShell hello tooexecute utilizzati.</span><span class="sxs-lookup"><span data-stu-id="367b3-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="367b3-188">Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="367b3-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="367b3-189">Seguire le istruzioni di hello per [caricando un toohello certificato API di Gestione portale di Azure classico](../azure-api-management-certs.md)e convalidare una configurazione delle credenziali con risorse di distribuzione classica hello utilizzando hello [codice di esempio tooauthenticate con risorse sulla distribuzione di Azure classico](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="367b3-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="367b3-190">Se è stato eseguito *non* creare un classico account RunAs, l'autenticazione con le risorse di gestione delle risorse e convalidare la configurazione di credenziali di hello utilizzando hello [codice per l'autenticazione con gestione del servizio di esempio risorse](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="367b3-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="367b3-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="367b3-191">Next steps</span></span>
* <span data-ttu-id="367b3-192">Per ulteriori informazioni sulle entità servizio, vedere troppo[oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="367b3-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="367b3-193">Per ulteriori informazioni sui certificati e i servizi di Azure, vedere troppo[panoramica dei certificati per servizi Cloud di Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="367b3-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
