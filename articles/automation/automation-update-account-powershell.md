---
title: Creare l'account RunAs di Automazione di Azure con PowerShell | Microsoft Docs
description: "Questo articolo descrive come aggiornare l'account di Automazione con PowerShell per creare gli account RunAs se questo passaggio non è stato eseguito durante la creazione iniziale nel portale."
services: automation
documentationcenter: 
author: eslesar
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
ms.openlocfilehash: fb23b3ea41910687fd586f80e5dd327344991e0f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a>Aggiornare l'account RunAs di Automazione con PowerShell
È possibile usare PowerShell per aggiornare l'account di Automazione esistente se:

* Si crea un account di Automazione ma si sceglie di non creare l'account RunAs.
* Si usa già un account di Automazione per gestire le risorse di Resource Manager e lo si vuole aggiornare per includere l'account RunAs per l'autenticazione dei runbook.
* Si usa già un account di Automazione per gestire le risorse classiche e lo si vuole aggiornare per usare l'account RunAs classico anziché creare un nuovo account ed eseguire la migrazione di runbook e asset nel nuovo account.   
* Si vuole creare un account RunAs e un account RunAs classico usando un certificato rilasciato dall'autorità di certificazione globale (enterprise).

## <a name="prerequisites"></a>Prerequisiti

* Lo script può essere eseguito solo in Windows 10 e Windows Server 2016 con i moduli di Azure Resource Manager 2.01 e versioni successive. Non sono supportate le versioni precedenti di Windows.
* Azure PowerShell 1.0 e versioni successive. Per informazioni su PowerShell 1.0, vedere [come installare e configurare Azure PowerShell](/powershell/azure/overview).
* Un account di automazione, a cui viene fatto riferimento come valore per i parametri *-AutomationAccountName* e *-ApplicationDisplayName* nello script di PowerShell seguente.

Per ottenere i valori per i parametri *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, obbligatori per gli script, seguire questa procedura:
1. Nel portale di Azure scegliere l'account di Automazione nel pannello **Account di Automazione** e selezionare **Tutte le impostazioni**. 
2. Nel pannello **Tutte le impostazioni** selezionare **Proprietà** in **Impostazioni account**. 
3. Prendere nota dei valori nel pannello **Proprietà**.

![Pannello "Proprietà" dell'account di Automazione](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a>Creare lo script di PowerShell per l'account RunAs
Questo script di PowerShell include il supporto per le configurazioni seguenti:

* Creare un account RunAs usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato enterprise.
* Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici.

A seconda dell'opzione di configurazione selezionata, lo script crea gli elementi riportati di seguito.

**Per gli account RunAs:**

* Crea un'applicazione Azure AD da esportare con la chiave pubblica del certificato autofirmato o enterprise. Crea un account dell'entità servizio per l'applicazione in Azure AD e assegna il ruolo Collaboratore per l'account nella sottoscrizione corrente. È possibile cambiare l'impostazione in Proprietario o in qualsiasi altro ruolo. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).
* Crea un asset di certificato di Automazione denominato *AzureRunAsCertificate* nell'account di Automazione specificato. L'asset di certificato contiene la chiave privata del certificato usata dall'applicazione Azure AD.
* Crea un asset di connessione di Automazione denominato *AzureRunAsConnection* nell'account di Automazione specificato. L'asset di connessione contiene l'ID applicazione, l'ID tenant, l'ID sottoscrizione e l'identificazione personale del certificato.

**Per gli account RunAs classici:**

* Crea un asset di certificato di Automazione denominato *AzureClassicRunAsCertificate* nell'account di Automazione specificato. L'asset di certificato contiene la chiave privata del certificato usata dal certificato di gestione.
* Crea un asset di connessione di Automazione denominato *AzureClassicRunAsConnection* nell'account di Automazione specificato. L'asset di connessione contiene il nome della sottoscrizione, l'ID sottoscrizione e il nome dell'asset di certificato.

>[!NOTE]
> Se si seleziona una delle due opzioni per creare l'account RunAs classico, dopo l'esecuzione dello script è necessario caricare il certificato pubblico, con estensione cer, nell'archivio di gestione della sottoscrizione in cui è stato creato l'account di Automazione.
> 

1. Salvare lo script seguente nel computer. Per questo esempio, salvare il file con il nome *New-RunAsAccount.ps1*.

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

2. Avviare **Windows PowerShell** con diritti utente elevati nel computer dalla schermata **Start**.
3. Nella shell della riga di comando con privilegi elevati passare alla cartella contenente lo script creato nel passaggio 1.  
4. Eseguire lo script usando i valori dei parametri per la configurazione richiesta.

    **Creare un account RunAs usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Creare un account RunAs e un account RunAs classico usando un certificato enterprise**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Creare un account RunAs e un account RunAs classico usando un certificato autofirmato nel cloud di Azure per enti pubblici**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Dopo l'esecuzione dello script, viene richiesto di autenticarsi con Azure. Accedere con un account membro del ruolo Amministratori della sottoscrizione e coamministratore della sottoscrizione.
    >
    >

Al termine dell'esecuzione dello script, tenere presente quanto segue:
* Se è stato creato un account RunAs classico con un certificato pubblico autofirmato, con estensione cer, lo script lo crea e lo salva nella cartella dei file temporanei del computer con il profilo utente *%USERPROFILE%\AppData\Local\Temp*, usato per eseguire la sessione di PowerShell.
* Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato. Seguire le istruzioni per [caricare un certificato dell'API di gestione nel portale di Azure classico](../azure-api-management-certs.md) e quindi usare il [codice di esempio per l'autenticazione con le risorse della distribuzione classica di Azure](automation-verify-runas-authentication.md#classic-run-as-authentication) per convalidare la configurazione delle credenziali con tali risorse. 
* Se *non* è stato creato un account RunAs classico, eseguire l'autenticazione con le risorse di Resource Manager e convalidare la configurazione delle credenziali usando il [codice di esempio per l'autenticazione con le risorse di Service Management](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sulle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).
* Per altre informazioni sui certificati e i servizi di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](../cloud-services/cloud-services-certs-create.md).
