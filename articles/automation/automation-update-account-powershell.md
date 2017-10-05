---
title: Creare l'account RunAs di Automazione di Azure con PowerShell | Microsoft Docs
description: "Questo articolo descrive come aggiornare l'account di Automazione con PowerShell per creare gli account RunAs se questo passaggio non è stato eseguito durante la creazione iniziale nel portale."
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
ms.openlocfilehash: a41a57ee3815a815c23e9bbe2dd0309e6c61c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="a86dd-103">Aggiornare l'account RunAs di Automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86dd-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="a86dd-104">È possibile usare PowerShell per aggiornare l'account di Automazione esistente se:</span><span class="sxs-lookup"><span data-stu-id="a86dd-104">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="a86dd-105">Si crea un account di Automazione ma si sceglie di non creare l'account RunAs.</span><span class="sxs-lookup"><span data-stu-id="a86dd-105">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="a86dd-106">Si usa già un account di Automazione per gestire le risorse di Resource Manager e lo si vuole aggiornare per includere l'account RunAs per l'autenticazione dei runbook.</span><span class="sxs-lookup"><span data-stu-id="a86dd-106">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="a86dd-107">Si usa già un account di Automazione per gestire le risorse classiche e lo si vuole aggiornare per usare l'account RunAs classico anziché creare un nuovo account ed eseguire la migrazione di runbook e asset nel nuovo account.</span><span class="sxs-lookup"><span data-stu-id="a86dd-107">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="a86dd-108">Si vuole creare un account RunAs e un account RunAs classico usando un certificato rilasciato dall'autorità di certificazione globale (enterprise).</span><span class="sxs-lookup"><span data-stu-id="a86dd-108">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a86dd-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a86dd-109">Prerequisites</span></span>

* <span data-ttu-id="a86dd-110">Lo script può essere eseguito solo in Windows 10 e Windows Server 2016 con i moduli di Azure Resource Manager 2.01 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a86dd-110">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="a86dd-111">Non sono supportate le versioni precedenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="a86dd-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="a86dd-112">Azure PowerShell 1.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a86dd-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="a86dd-113">Per informazioni su PowerShell 1.0, vedere [come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a86dd-113">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a86dd-114">Un account di automazione, a cui viene fatto riferimento come valore per i parametri *-AutomationAccountName* e *-ApplicationDisplayName* nello script di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="a86dd-114">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="a86dd-115">Per ottenere i valori per i parametri *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, obbligatori per gli script, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a86dd-115">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="a86dd-116">Nel portale di Azure scegliere l'account di Automazione nel pannello **Account di Automazione** e selezionare **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a86dd-116">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="a86dd-117">Nel pannello **Tutte le impostazioni** selezionare **Proprietà** in **Impostazioni account**.</span><span class="sxs-lookup"><span data-stu-id="a86dd-117">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="a86dd-118">Prendere nota dei valori nel pannello **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="a86dd-118">Note the values on the **Properties** blade.</span></span>

![Pannello "Proprietà" dell'account di Automazione](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="a86dd-120">Creare lo script di PowerShell per l'account RunAs</span><span class="sxs-lookup"><span data-stu-id="a86dd-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="a86dd-121">Questo script di PowerShell include il supporto per le configurazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a86dd-121">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="a86dd-122">Creare un account RunAs usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a86dd-123">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="a86dd-124">Creare un account RunAs e un account RunAs classico usando un certificato enterprise.</span><span class="sxs-lookup"><span data-stu-id="a86dd-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="a86dd-125">Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="a86dd-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="a86dd-126">A seconda dell'opzione di configurazione selezionata, lo script crea gli elementi riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="a86dd-126">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="a86dd-127">**Per gli account RunAs:**</span><span class="sxs-lookup"><span data-stu-id="a86dd-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="a86dd-128">Crea un'applicazione Azure AD da esportare con la chiave pubblica del certificato autofirmato o enterprise. Crea un account dell'entità servizio per l'applicazione in Azure AD e assegna il ruolo Collaboratore per l'account nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="a86dd-128">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="a86dd-129">È possibile cambiare l'impostazione in Proprietario o in qualsiasi altro ruolo.</span><span class="sxs-lookup"><span data-stu-id="a86dd-129">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="a86dd-130">Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a86dd-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="a86dd-131">Crea un asset di certificato di Automazione denominato *AzureRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a86dd-132">L'asset di certificato contiene la chiave privata del certificato usata dall'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a86dd-132">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="a86dd-133">Crea un asset di connessione di Automazione denominato *AzureRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-133">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a86dd-134">L'asset di connessione contiene l'ID applicazione, l'ID tenant, l'ID sottoscrizione e l'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-134">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="a86dd-135">**Per gli account RunAs classici:**</span><span class="sxs-lookup"><span data-stu-id="a86dd-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="a86dd-136">Crea un asset di certificato di Automazione denominato *AzureClassicRunAsCertificate* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="a86dd-137">L'asset di certificato contiene la chiave privata del certificato usata dal certificato di gestione.</span><span class="sxs-lookup"><span data-stu-id="a86dd-137">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="a86dd-138">Crea un asset di connessione di Automazione denominato *AzureClassicRunAsConnection* nell'account di Automazione specificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="a86dd-139">L'asset di connessione contiene il nome della sottoscrizione, l'ID sottoscrizione e il nome dell'asset di certificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-139">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="a86dd-140">Se si seleziona una delle due opzioni per creare l'account RunAs classico, dopo l'esecuzione dello script è necessario caricare il certificato pubblico, con estensione cer, nell'archivio di gestione della sottoscrizione in cui è stato creato l'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="a86dd-140">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

1. <span data-ttu-id="a86dd-141">Salvare lo script seguente nel computer.</span><span class="sxs-lookup"><span data-stu-id="a86dd-141">Save the following script on your computer.</span></span> <span data-ttu-id="a86dd-142">Per questo esempio, salvare il file con il nome *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="a86dd-142">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="a86dd-143">Avviare **Windows PowerShell** con diritti utente elevati nel computer dalla schermata **Start**.</span><span class="sxs-lookup"><span data-stu-id="a86dd-143">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="a86dd-144">Nella shell della riga di comando con privilegi elevati passare alla cartella contenente lo script creato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="a86dd-144">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
4. <span data-ttu-id="a86dd-145">Eseguire lo script usando i valori dei parametri per la configurazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="a86dd-145">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="a86dd-146">**Creare un account RunAs usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="a86dd-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="a86dd-147">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**</span><span class="sxs-lookup"><span data-stu-id="a86dd-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="a86dd-148">**Creare un account RunAs e un account RunAs classico usando un certificato enterprise**</span><span class="sxs-lookup"><span data-stu-id="a86dd-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="a86dd-149">**Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici**</span><span class="sxs-lookup"><span data-stu-id="a86dd-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="a86dd-150">Dopo l'esecuzione dello script, viene richiesto di autenticarsi con Azure.</span><span class="sxs-lookup"><span data-stu-id="a86dd-150">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="a86dd-151">Accedere con un account membro del ruolo Amministratori della sottoscrizione e coamministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a86dd-151">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="a86dd-152">Al termine dell'esecuzione dello script, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a86dd-152">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="a86dd-153">Se è stato creato un account RunAs classico con un certificato pubblico autofirmato, con estensione cer, lo script lo crea e lo salva nella cartella dei file temporanei del computer con il profilo utente *%USERPROFILE%\AppData\Local\Temp*, usato per eseguire la sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a86dd-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="a86dd-154">Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato.</span><span class="sxs-lookup"><span data-stu-id="a86dd-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="a86dd-155">Seguire le istruzioni per [caricare un certificato dell'API di gestione nel portale di Azure classico](../azure-api-management-certs.md) e quindi usare il [codice di esempio per l'autenticazione con le risorse della distribuzione classica di Azure](automation-verify-runas-authentication.md#classic-run-as-authentication) per convalidare la configurazione delle credenziali con tali risorse.</span><span class="sxs-lookup"><span data-stu-id="a86dd-155">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with classic deployment resources by using the [sample code to authenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="a86dd-156">Se *non* è stato creato un account RunAs classico, eseguire l'autenticazione con le risorse di Resource Manager e convalidare la configurazione delle credenziali usando il [codice di esempio per l'autenticazione con le risorse di Service Management](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="a86dd-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86dd-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a86dd-157">Next steps</span></span>
* <span data-ttu-id="a86dd-158">Per altre informazioni sulle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a86dd-158">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="a86dd-159">Per altre informazioni sui certificati e i servizi di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a86dd-159">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
