---
title: Creare account RunAs di Automazione di Azure | Microsoft Docs
description: Questo articolo descrive come aggiornare l'account di Automazione e creare account RunAs con PowerShell o dal portale.
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
ms.openlocfilehash: eaf6eb49bbfe4572827fcc101d1f552b48ab91e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="32b35-103">Aggiornare l'autenticazione dell'account di Automazione con account RunAs</span><span class="sxs-lookup"><span data-stu-id="32b35-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="32b35-104">È possibile aggiornare l'account di Automazione esistente dal portale o con PowerShell se:</span><span class="sxs-lookup"><span data-stu-id="32b35-104">You can update your existing Automation account from the portal or use PowerShell if:</span></span>

* <span data-ttu-id="32b35-105">Si crea un account di Automazione ma si sceglie di non creare l'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="32b35-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="32b35-106">Si usa già un account di Automazione per gestire le risorse di Resource Manager e lo si vuole aggiornare per includere l'account RunAs per l'autenticazione dei runbook.</span><span class="sxs-lookup"><span data-stu-id="32b35-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="32b35-107">Si usa già un account di Automazione per gestire le risorse classiche e lo si vuole aggiornare per usare l'account RunAs classico anziché creare un nuovo account ed eseguire la migrazione di runbook e asset nel nuovo account.</span><span class="sxs-lookup"><span data-stu-id="32b35-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="32b35-108">Si vuole creare un account RunAs e un account RunAs classico usando un certificato rilasciato dall'autorità di certificazione globale (enterprise).</span><span class="sxs-lookup"><span data-stu-id="32b35-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32b35-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32b35-109">Prerequisites</span></span>

* <span data-ttu-id="32b35-110">Lo script può essere eseguito solo in Windows 10 e Windows Server 2016 con i moduli di Azure Resource Manager 3.0.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="32b35-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="32b35-111">Non sono supportate le versioni precedenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="32b35-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="32b35-112">Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="32b35-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="32b35-113">Per informazioni su PowerShell 1.0, vedere [come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="32b35-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="32b35-114">Un account di automazione, a cui viene fatto riferimento come valore per i parametri *-AutomationAccountName* e *-ApplicationDisplayName* nello script di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="32b35-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="32b35-115">Per ottenere i valori per i parametri *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, obbligatori per gli script, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="32b35-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="32b35-116">Nel portale di Azure scegliere l'account di Automazione nel pannello **Account di Automazione** e selezionare **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="32b35-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="32b35-117">Nel pannello **Tutte le impostazioni** selezionare **Proprietà** in **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="32b35-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="32b35-118">Prendere nota dei valori nel pannello **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="32b35-118">Note the values on the **Properties** blade.</span></span><br><br> <span data-ttu-id="32b35-119">![Pannello "Proprietà" dell'account di Automazione](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="32b35-119">![The Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-to-update-your-automation-account"></a><span data-ttu-id="32b35-120">Autorizzazioni necessarie per l'aggiornamento dell'account di Automazione</span><span class="sxs-lookup"><span data-stu-id="32b35-120">Required permissions to update your Automation account</span></span>
<span data-ttu-id="32b35-121">Per aggiornare un account di Automazione, è necessario avere le autorizzazioni e i privilegi specifici seguenti, necessari per il completamento di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="32b35-121">To update an Automation account, you must have the following specific privileges and permissions required to complete this topic.</span></span>   
 
* <span data-ttu-id="32b35-122">L'account utente di AD deve essere aggiunto a un ruolo con autorizzazioni equivalenti al ruolo Collaboratore per le risorse di Microsoft.Automation, come indicato nell'articolo [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="32b35-122">Your AD user account needs to be added to a role with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="32b35-123">Gli utenti non amministratori nel tenant di Azure AD possono [registrare le applicazioni di AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se le impostazioni delle registrazioni dell'app sono impostate su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="32b35-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the App registrations setting is set to **Yes**.</span></span>  <span data-ttu-id="32b35-124">Se le impostazioni delle registrazioni dell'app sono impostate su **No**, l'utente che esegue questa azione deve essere un amministratore globale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32b35-124">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="32b35-125">Se l'utente non è membro dell'istanza di Active Directory della sottoscrizione prima dell'aggiunta al ruolo di amministratore globale/coamministratore della sottoscrizione, viene aggiunto ad Active Directory come guest.</span><span class="sxs-lookup"><span data-stu-id="32b35-125">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="32b35-126">In questa situazione si riceve un avviso di tipo "L'utente non è autorizzato a creare..."</span><span class="sxs-lookup"><span data-stu-id="32b35-126">In this situation, you receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="32b35-127">nel pannello **Aggiungi account di Automazione**.</span><span class="sxs-lookup"><span data-stu-id="32b35-127">warning on the **Add Automation Account** blade.</span></span> <span data-ttu-id="32b35-128">Gli utenti che prima sono stati aggiunti al ruolo di amministratore globale/coamministratore possono essere rimossi dall'istanza di Active Directory della sottoscrizione e aggiunti nuovamente per renderli utenti completi in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32b35-128">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="32b35-129">Per verificare questa situazione dal riquadro **Azure Active Directory** nel portale di Azure selezionare **Utenti e gruppi**, **Tutti gli utenti** e, dopo avere selezionato l'utente specifico, selezionare **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="32b35-129">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="32b35-130">Il valore dell'attributo **Tipo utente** nel profilo utente non deve essere **Guest**.</span><span class="sxs-lookup"><span data-stu-id="32b35-130">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-the-portal"></a><span data-ttu-id="32b35-131">Creare un account RunAs dal portale</span><span class="sxs-lookup"><span data-stu-id="32b35-131">Create Run As account from the portal</span></span>
<span data-ttu-id="32b35-132">La procedura descritta in questa sezione consente di aggiornare un account di Automazione di Azure dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32b35-132">In this section, perform the following steps to update your Azure Automation account from  the Azure portal.</span></span>  <span data-ttu-id="32b35-133">Creare gli account RunAs e RunAs classico separatamente; se non è necessario gestire risorse nel portale di Azure classico, è possibile creare solo l'account RunAs di Azure.</span><span class="sxs-lookup"><span data-stu-id="32b35-133">You create the Run As and Classic Run As accounts individually, and if you don't need to manage resources in the classic Azure portal, you can just create the Azure Run As account.</span></span>  

<span data-ttu-id="32b35-134">Questo processo crea gli elementi seguenti nell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="32b35-134">The process creates the following items in your Automation account.</span></span>

<span data-ttu-id="32b35-135">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="32b35-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="32b35-136">Crea un'applicazione Azure AD da esportare con un certificato autofirmato, crea un account dell'entità servizio per l'applicazione in Azure AD e assegna il ruolo Collaboratore per l'account nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="32b35-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="32b35-137">È possibile cambiare l'impostazione in Proprietario o in qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="32b35-137">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="32b35-138">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="32b35-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="32b35-139">Crea un asset di certificato di Automazione denominato *AzureRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="32b35-140">L'asset di certificato contiene la chiave privata del certificato usata dall'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32b35-140">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="32b35-141">Crea un asset di connessione di Automazione denominato *AzureRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-141">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="32b35-142">L'asset di connessione contiene l'ID applicazione, l'ID tenant, l'ID sottoscrizione e l'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-142">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="32b35-143">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="32b35-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="32b35-144">Crea un asset di certificato di Automazione denominato *AzureClassicRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="32b35-145">L'asset di certificato contiene la chiave privata del certificato usata dal certificato di gestione.</span><span class="sxs-lookup"><span data-stu-id="32b35-145">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="32b35-146">Crea un asset di connessione di Automazione denominato *AzureClassicRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="32b35-147">L'asset di connessione contiene il nome della sottoscrizione, l'ID sottoscrizione e il nome dell'asset di certificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-147">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="32b35-148">Accedere al Portale di Azure con un account membro del ruolo Amministratori della sottoscrizione e coamministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="32b35-148">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
2. <span data-ttu-id="32b35-149">Nel pannello Account di automazione, selezionare **Account RunAs** nella sezione **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="32b35-149">From the Automation account blade, select **Run As Accounts** under the section **Account Settings**.</span></span>  
3. <span data-ttu-id="32b35-150">A seconda del tipo di account necessario, selezionare **Account RunAs di Azure** o **Account RunAs classico di Azure**.</span><span class="sxs-lookup"><span data-stu-id="32b35-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="32b35-151">Dopo aver selezionato **Account RunAs di Azure** o **Account RunAs classico di Azure**, viene visualizzato il pannello corrispondente. Rivedere le informazioni generali e fare clic su **Crea** per procedere con la creazione dell'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="32b35-151">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
4. <span data-ttu-id="32b35-152">Mentre Azure crea l'account RunAs, è possibile tenere traccia dello stato di avanzamento scegliendo **Notifiche** dal menu. Verrà visualizzato un banner per indicare che l'account è in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="32b35-152">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu and a banner is displayed stating the account is being created.</span></span>  <span data-ttu-id="32b35-153">Il processo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="32b35-153">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="32b35-154">Creare un account RunAs usando lo script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="32b35-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="32b35-155">Questo script di PowerShell include il supporto per le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="32b35-155">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="32b35-156">Creare un account RunAs usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="32b35-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="32b35-157">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="32b35-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="32b35-158">Creare un account RunAs e un account RunAs classico usando un certificato enterprise.</span><span class="sxs-lookup"><span data-stu-id="32b35-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="32b35-159">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="32b35-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="32b35-160">A seconda dell'opzione di configurazione selezionata, lo script crea gli elementi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="32b35-160">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="32b35-161">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="32b35-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="32b35-162">Crea un'applicazione Azure AD da esportare con la chiave pubblica del certificato autofirmato o enterprise. Crea un account dell'entità servizio per l'applicazione in Azure AD e assegna il ruolo Collaboratore per l'account nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="32b35-162">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="32b35-163">È possibile cambiare l'impostazione in Proprietario o in qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="32b35-163">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="32b35-164">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="32b35-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="32b35-165">Crea un asset di certificato di Automazione denominato *AzureRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="32b35-166">L'asset di certificato contiene la chiave privata del certificato usata dall'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32b35-166">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="32b35-167">Crea un asset di connessione di Automazione denominato *AzureRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-167">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="32b35-168">L'asset di connessione contiene l'ID applicazione, l'ID tenant, l'ID sottoscrizione e l'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-168">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="32b35-169">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="32b35-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="32b35-170">Crea un asset di certificato di Automazione denominato *AzureClassicRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="32b35-171">L'asset di certificato contiene la chiave privata del certificato usata dal certificato di gestione.</span><span class="sxs-lookup"><span data-stu-id="32b35-171">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="32b35-172">Crea un asset di connessione di Automazione denominato *AzureClassicRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="32b35-173">L'asset di connessione contiene il nome della sottoscrizione, l'ID sottoscrizione e il nome dell'asset di certificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-173">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="32b35-174">Se si seleziona una delle due opzioni per creare l'account RunAs classico, dopo l'esecuzione dello script è necessario caricare il certificato pubblico, con estensione cer, nell'archivio di gestione della sottoscrizione in cui è stato creato l'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="32b35-174">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="32b35-175">Salvare lo script seguente nel computer.</span><span class="sxs-lookup"><span data-stu-id="32b35-175">Save the following script on your computer.</span></span> <span data-ttu-id="32b35-176">Per questo esempio, salvare il file con il nome *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="32b35-176">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
            Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                     "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="32b35-177">Avviare **Windows PowerShell** con diritti utente elevati nel computer dalla schermata **Start**.</span><span class="sxs-lookup"><span data-stu-id="32b35-177">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="32b35-178">Nella shell della riga di comando con privilegi elevati passare alla cartella contenente lo script creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="32b35-178">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="32b35-179">Eseguire lo script usando i valori dei parametri per la configurazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="32b35-179">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="32b35-180">**Creare un account RunAs usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="32b35-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="32b35-181">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="32b35-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="32b35-182">**Creare un account RunAs e un account RunAs classico usando un certificato enterprise**</span><span class="sxs-lookup"><span data-stu-id="32b35-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="32b35-183">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici**</span><span class="sxs-lookup"><span data-stu-id="32b35-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="32b35-184">Dopo l'esecuzione dello script, viene richiesto di autenticarsi con Azure.</span><span class="sxs-lookup"><span data-stu-id="32b35-184">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="32b35-185">Accedere con un account membro del ruolo Amministratori della sottoscrizione e coamministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="32b35-185">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="32b35-186">Al termine dell'esecuzione dello script, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="32b35-186">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="32b35-187">Se è stato creato un account RunAs classico con un certificato pubblico autofirmato, con estensione cer, lo script lo crea e lo salva nella cartella dei file temporanei del computer con il profilo utente *%USERPROFILE%\AppData\Local\Temp*, usato per eseguire la sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32b35-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="32b35-188">Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="32b35-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="32b35-189">Seguire le istruzioni per [caricare un certificato dell'API di gestione nel portale di Azure classico](../azure-api-management-certs.md) e quindi usare il [codice di esempio per l'autenticazione con le risorse della distribuzione classica di Azure](automation-verify-runas-authentication.md#classic-run-as-authentication) per convalidare la configurazione delle credenziali con tali risorse.</span><span class="sxs-lookup"><span data-stu-id="32b35-189">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="32b35-190">Se *non* è stato creato un account RunAs classico, eseguire l'autenticazione con le risorse di Resource Manager e convalidare la configurazione delle credenziali usando il [codice di esempio per l'autenticazione con le risorse di Service Management](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="32b35-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b35-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32b35-191">Next steps</span></span>
* <span data-ttu-id="32b35-192">Per altre informazioni sulle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="32b35-192">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="32b35-193">Per altre informazioni sui certificati e i servizi di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="32b35-193">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>