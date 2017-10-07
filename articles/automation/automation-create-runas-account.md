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
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Aggiornare l'autenticazione dell'account di Automazione con account RunAs 
È possibile aggiornare l'account di automazione esistente dal portale hello o se l'utilizzo di PowerShell:

* Si crea un account di automazione, ma rifiuta toocreate account RunAs hello.
* Già in uso un risorse di gestione risorse di automazione account toomanage e si desidera tooupdate hello account tooinclude hello account RunAs per l'autenticazione di runbook.
* Già in uso un'automazione account toomanage classico alle risorse e si desidera tooupdate è toouse hello Classic account RunAs anziché creare un nuovo account e la migrazione tooit i runbook e le risorse.   
* Si desidera toocreate Esegui come e un classico account RunAs utilizzando un certificato rilasciato dall'autorità di certificazione dell'organizzazione (CA).

## <a name="prerequisites"></a>Prerequisiti

* Hello script può essere eseguito solo in Windows 10 e Windows Server 2016 con moduli di gestione risorse di Azure 3.0.0 e versioni successive. Non sono supportate le versioni precedenti di Windows.
* Azure PowerShell 1.0 e versioni successive. Per informazioni sulla versione di hello PowerShell 1.0, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).
* Un account di automazione cui viene fatto riferimento come valore hello hello *– AutomationAccountName* e *- ApplicationDisplayName* parametri hello lo script di PowerShell seguente.

i valori hello tooget per *SubscriptionID*, *gruppo di risorse*, e *AutomationAccountName*, che sono parametri obbligatori per lo script hello, hello seguenti:

1. In hello portale di Azure, selezionare l'account di automazione in hello **account di automazione** blade e quindi selezionare **tutte le impostazioni**.  
2. In hello **tutte le impostazioni** pannello, in **impostazioni Account**selezionare **proprietà**. 
3. Notare i valori hello in hello **proprietà** blade.<br><br> ![Pannello di "Proprietà" Hello automazione account](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-tooupdate-your-automation-account"></a>Necessarie autorizzazioni tooupdate l'account di automazione
tooupdate un account di automazione, è necessario disporre di privilegi specifici seguenti hello e le autorizzazioni necessarie toocomplete in questo argomento.   
 
* L'account utente di Active Directory deve toobe tooa aggiunto ruolo con ruolo di collaboratore toohello equivalenti autorizzazioni per le risorse di Microsoft, come illustrato nell'articolo [controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md#contributor-role-permissions).  
* Gli utenti senza privilegi di amministratore nel tenant di Azure AD possono [registrare applicazioni AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se registrazioni di App hello impostazione è troppo**Sì**.  Se le registrazioni di app hello impostazione è troppo**n**, utente hello eseguendo questa azione deve essere un amministratore globale di Azure AD. 

Se non si un membro di istanza di Active Directory della sottoscrizione hello prima dell'aggiunta di toohello amministratore/coamministratore ruolo globale della sottoscrizione di hello, tooActive Directory aggiunti come guest. In questo caso, viene visualizzato un "non si dispone delle autorizzazioni toocreate..." visualizzazione dell'avviso hello **aggiungere Account di automazione** blade. Gli utenti che sono stati aggiunti toohello amministratore/coamministratore ruolo globale può essere rimosso dall'istanza di Active Directory della sottoscrizione hello e riaggiunto toomake prima li un utente in Active Directory completa. tooverify tale situazione, hello **Azure Active Directory** riquadro nel portale di Azure selezionare hello **utenti e gruppi**selezionare **tutti gli utenti** e, dopo aver selezionato hello un utente specifico, seleziona **profilo**. valore di hello Hello **tipo utente** attributo del profilo utenti hello non deve essere uguale **Guest**.

## <a name="create-run-as-account-from-hello-portal"></a>Creare account RunAs dal portale hello
In questa sezione, eseguire hello seguendo i passaggi tooupdate l'account di automazione di Azure dal portale di Azure hello.  Creerai hello account RunAs e classico runas singolarmente, e se non sono necessarie risorse toomanage nel portale di Azure classico hello, è possibile creare hello Azure account RunAs.  

il processo di Hello crea hello elementi nell'account di automazione.

**Per gli account RunAs:**

* Crea un'applicazione Azure AD con un certificato autofirmato, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna il ruolo di collaboratore hello per conto di hello nella sottoscrizione corrente. È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).
* Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.
* Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.

**Per gli account RunAs classici:**

* Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.
* Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.

1. Accedi toohello portale di Azure con un account che sia un membro del ruolo di amministratori della sottoscrizione hello e al coamministratore della sottoscrizione hello.
2. Dal Pannello di account di automazione hello, selezionare **account RunAs** nella sezione hello **impostazioni Account**.  
3. A seconda del tipo di account necessario, selezionare **Account RunAs di Azure** o **Account RunAs classico di Azure**.  Dopo aver selezionato uno hello **aggiungere Azure runas** o **aggiungere Azure classico Account runas** pannello viene visualizzato e dopo aver esaminato le informazioni generali di hello, fare clic su **crea** tooproceed con la creazione di account RunAs.  
4. Mentre Azure crea account RunAs hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** da hello menu e un messaggio viene visualizzato indicante account hello viene creato.  Questo processo può richiedere alcuni minuti toocomplete.  

## <a name="create-run-as-account-using-powershell-script"></a>Creare un account RunAs usando lo script di PowerShell
Questo script di PowerShell include il supporto per hello seguenti configurazioni:

* Creare un account RunAs usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato autofirmato.
* Creare un account RunAs e un account RunAs classico usando un certificato enterprise.
* Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici.

A seconda opzione di configurazione hello selezionata, lo script di hello crea hello seguenti elementi.

**Per gli account RunAs:**

* Crea un Azure AD applicazione toobe esportato con entrambi hello autofirmato o chiave pubblica del certificato dell'organizzazione, crea un account dell'entità servizio per un'applicazione hello in Azure AD e assegna hello ruolo Collaboratore per conto di hello in corrente sottoscrizione. È possibile modificare questa impostazione tooOwner o qualsiasi altro ruolo. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo in Automazione di Azure](automation-role-based-access-control.md).
* Crea un asset del certificato di automazione denominato *AzureRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato da un'applicazione hello Azure AD.
* Crea un asset connessione di automazione denominato *AzureRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello applicationId, tenantId, ID sottoscrizione e identificazione personale del certificato.

**Per gli account RunAs classici:**

* Crea un asset del certificato di automazione denominato *AzureClassicRunAsCertificate* in hello specificato l'account di automazione. asset del certificato di Hello contiene hello chiave privata del certificato utilizzato dal certificato di gestione di hello.
* Crea un asset connessione di automazione denominato *AzureClassicRunAsConnection* in hello specificato l'account di automazione. asset della connessione di Hello contiene hello sottoscrizione nome, ID sottoscrizione e nome dell'asset certificato.

>[!NOTE]
> Se si seleziona l'opzione desiderata per la creazione di un classico account RunAs, dopo l'esecuzione di script hello, caricamento hello pubblica Gestione toohello (estensione del nome file con estensione cer) dell'archivio certificati per la sottoscrizione di hello che hello account di automazione è stato creato.
> 

1. Salvare lo script seguente nel computer in uso hello. In questo esempio, salvarlo con il nome file hello *New RunAsAccount.ps1*.

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

2. Nel computer, avviare **Windows PowerShell** da hello **avviare** schermata con diritti utente elevati.
3. Da hello elevati shell della riga di comando, passare toohello cartella che contiene lo script hello creato nel passaggio 1.  
4. Eseguire script hello utilizzando i valori dei parametri hello per la configurazione di hello desiderate.

    **Creare un account RunAs usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Creare un account RunAs e un account RunAs classico usando un certificato autofirmato**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Creare un account RunAs e un account RunAs classico usando un certificato enterprise**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Creare un account RunAs e un classico account RunAs utilizzando un certificato autofirmato in hello cloud di Azure per enti pubblici**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Dopo l'esecuzione di script hello è, sarà richiesta tooauthenticate con Azure. Accedere con un account che sia un membro del ruolo amministratori di sottoscrizione hello e al coamministratore della sottoscrizione hello.
    >
    >

Dopo l'esecuzione dello script hello completata, si noti seguenti hello:
* Se è stato creato un classico account RunAs con un certificato pubblico autofirmato (file con estensione cer), script hello crea e Salva toohello cartella dei file temporanei nel computer in uso nel profilo utente hello *%USERPROFILE%\AppData\Local\Temp*, sessione di PowerShell hello tooexecute utilizzati.
* Se è stato creato un account RunAs classico con un certificato pubblico enterprise, con estensione cer, usare questo certificato. Seguire le istruzioni di hello per [caricando un toohello certificato API di Gestione portale di Azure classico](../azure-api-management-certs.md)e convalidare una configurazione delle credenziali con risorse di distribuzione classica hello utilizzando hello [codice di esempio tooauthenticate con risorse sulla distribuzione di Azure classico](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Se è stato eseguito *non* creare un classico account RunAs, l'autenticazione con le risorse di gestione delle risorse e convalidare la configurazione di credenziali di hello utilizzando hello [codice per l'autenticazione con gestione del servizio di esempio risorse](automation-verify-runas-authentication.md#automation-run-as-authentication).

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sulle entità servizio, vedere troppo[oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).
* Per ulteriori informazioni sui certificati e i servizi di Azure, vedere troppo[panoramica dei certificati per servizi Cloud di Azure](../cloud-services/cloud-services-certs-create.md).
