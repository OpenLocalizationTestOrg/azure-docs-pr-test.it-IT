---
title: account di automazione runas di Azure con PowerShell aaaCreate | Documenti Microsoft
description: "In questo articolo viene descritto come tooupgrade l'account di automazione con PowerShell toocreate hello Run As account se non si è eseguito questo passaggio durante la creazione iniziale dal portale hello."
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="cd066-103">Aggiornare l'account RunAs di Automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd066-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="cd066-104">È possibile utilizzare l'account di automazione esistente PowerShell tooupdate se:</span><span class="sxs-lookup"><span data-stu-id="cd066-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="cd066-105">Si crea un account di automazione, ma rifiuta toocreate account RunAs hello.</span><span class="sxs-lookup"><span data-stu-id="cd066-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="cd066-106">Già in uso un risorse di gestione risorse di automazione account toomanage e si desidera tooupdate hello account tooinclude hello account RunAs per l'autenticazione di runbook.</span><span class="sxs-lookup"><span data-stu-id="cd066-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="cd066-107">Già in uso un'automazione account toomanage classico alle risorse e si desidera tooupdate è toouse hello Classic account RunAs anziché creare un nuovo account e la migrazione tooit i runbook e le risorse.</span><span class="sxs-lookup"><span data-stu-id="cd066-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="cd066-108">Si desidera toocreate Esegui come e un classico account RunAs utilizzando un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA).</span><span class="sxs-lookup"><span data-stu-id="cd066-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd066-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cd066-109">Prerequisites</span></span>

* <span data-ttu-id="cd066-110">script di Hello può essere eseguito solo in Windows 10 e Windows Server 2016 con moduli di gestione risorse di Azure 2.01 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cd066-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="cd066-111">Non sono supportate le versioni precedenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="cd066-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="cd066-112">Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cd066-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="cd066-113">Per informazioni sulla versione di hello PowerShell 1.0, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd066-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="cd066-114">Un account di automazione cui viene fatto riferimento come valore hello hello *– AutomationAccountName* e *- ApplicationDisplayName* parametri hello lo script di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="cd066-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="cd066-115">i valori hello tooget per *SubscriptionID*, *gruppo di risorse*, e *AutomationAccountName*, che sono parametri obbligatori per gli script hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cd066-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="cd066-116">In hello portale di Azure, selezionare l'account di automazione in hello **account di automazione** blade e quindi selezionare **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="cd066-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="cd066-117">In hello **tutte le impostazioni** pannello, in **impostazioni Account**selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="cd066-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="cd066-118">Notare i valori hello in hello **proprietà** blade.</span><span class="sxs-lookup"><span data-stu-id="cd066-118">Note hello values on hello **Properties** blade.</span></span>

![Pannello di "Proprietà" Hello automazione account](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="cd066-120">Creare lo script di PowerShell per l'account RunAs</span><span class="sxs-lookup"><span data-stu-id="cd066-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="cd066-121">Questo script di PowerShell include il supporto per hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="cd066-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="cd066-122">Creare un account RunAs usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="cd066-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="cd066-123">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="cd066-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="cd066-124">Creare un account RunAs e un account RunAs classico usando un certificato enterprise.</span><span class="sxs-lookup"><span data-stu-id="cd066-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="cd066-125">Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="cd066-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="cd066-126">A seconda opzione di configurazione hello selezionata, lo script di hello crea hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="cd066-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="cd066-127">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="cd066-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="cd066-128">Crea un Azure AD applicazione toobe esportato con entrambi hello autofirmato o chiave pubblica del certificato dell'organizzazione, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna hello ruolo Collaboratore per conto di hello in corrente sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cd066-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="cd066-129">È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="cd066-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="cd066-130">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="cd066-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="cd066-131">Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="cd066-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="cd066-132">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd066-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="cd066-133">Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="cd066-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="cd066-134">asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="cd066-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="cd066-135">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="cd066-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="cd066-136">Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="cd066-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="cd066-137">asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="cd066-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="cd066-138">Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="cd066-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="cd066-139">asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.</span><span class="sxs-lookup"><span data-stu-id="cd066-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="cd066-140">Se si seleziona l'opzione desiderata per la creazione di un classico account RunAs, dopo l'esecuzione di script hello, caricamento hello pubblica Gestione toohello (estensione del nome file con estensione cer) dell'archivio certificati per la sottoscrizione di hello che hello account di automazione è stato creato.</span><span class="sxs-lookup"><span data-stu-id="cd066-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="cd066-141">Salvare lo script seguente nel computer in uso hello.</span><span class="sxs-lookup"><span data-stu-id="cd066-141">Save hello following script on your computer.</span></span> <span data-ttu-id="cd066-142">In questo esempio, salvarlo con il nome file hello *New RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="cd066-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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

2. <span data-ttu-id="cd066-143">Nel computer, avviare **Windows PowerShell** da hello **avviare** schermata con diritti utente elevati.</span><span class="sxs-lookup"><span data-stu-id="cd066-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="cd066-144">Da hello elevati shell della riga di comando, passare toohello cartella che contiene lo script hello creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="cd066-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="cd066-145">Eseguire script hello utilizzando i valori dei parametri hello per la configurazione di hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="cd066-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="cd066-146">**Creare un account RunAs usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="cd066-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="cd066-147">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="cd066-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="cd066-148">**Creare un account RunAs e un account RunAs classico usando un certificato enterprise**</span><span class="sxs-lookup"><span data-stu-id="cd066-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="cd066-149">**Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici**</span><span class="sxs-lookup"><span data-stu-id="cd066-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="cd066-150">Dopo l'esecuzione di script hello è, sarà richiesta tooauthenticate con Azure.</span><span class="sxs-lookup"><span data-stu-id="cd066-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="cd066-151">Accedere con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="cd066-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="cd066-152">Dopo l'esecuzione dello script hello completata, si noti seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="cd066-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="cd066-153">Se è stato creato un classico account RunAs con un certificato pubblico autofirmato (file con estensione cer), script hello crea e Salva toohello cartella dei file temporanei nel computer in uso nel profilo utente hello *%USERPROFILE%\AppData\Local\Temp*, sessione di PowerShell hello tooexecute utilizzati.</span><span class="sxs-lookup"><span data-stu-id="cd066-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="cd066-154">Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="cd066-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="cd066-155">Seguire le istruzioni di hello per [caricando un toohello certificato API di Gestione portale di Azure classico](../azure-api-management-certs.md)e convalidare una configurazione delle credenziali con risorse di distribuzione classica hello utilizzando hello [codice di esempio tooauthenticate con risorse sulla distribuzione di Azure classico](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="cd066-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="cd066-156">Se è stato eseguito *non* creare un classico account RunAs, l'autenticazione con le risorse di gestione delle risorse e convalidare la configurazione di credenziali di hello utilizzando hello [codice per l'autenticazione con gestione del servizio di esempio risorse](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="cd066-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd066-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd066-157">Next steps</span></span>
* <span data-ttu-id="cd066-158">Per ulteriori informazioni sulle entità servizio, vedere troppo[oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="cd066-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="cd066-159">Per ulteriori informazioni sui certificati e i servizi di Azure, vedere troppo[panoramica dei certificati per servizi Cloud di Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="cd066-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
