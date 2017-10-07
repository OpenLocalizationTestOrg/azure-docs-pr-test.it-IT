---
title: "identità aaaCreate per app di Azure con PowerShell | Documenti Microsoft"
description: "Viene descritto come controllare toouse Azure PowerShell toocreate un'applicazione Azure Active Directory e dell'entità servizio e concedere tooresources accedere tramite l'accesso basato sui ruoli. Viene illustrato come applicazione tooauthenticate con un certificato o la password."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio

Quando si dispone di un'app o script che richiede risorse tooaccess, è possibile impostare un'identità per l'applicazione hello e l'applicazione hello con le proprie credenziali di autenticazione. Questa identità è nota come entità servizio. Questo approccio consente di:

* Assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni. In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.
* Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.

In questo argomento illustra come toouse [Azure PowerShell](/powershell/azure/overview) tooset le operazioni necessarie per un'applicazione toorun sotto le proprie credenziali e l'identità.

## <a name="required-permissions"></a>Autorizzazioni necessarie
toocomplete in questo argomento, è necessario disporre delle autorizzazioni sufficienti in Azure Active Directory sia la sottoscrizione di Azure. In particolare, devono essere in grado di toocreate un'app in Azure Active Directory hello e assegnazione di ruolo tooa principale di servizio hello. 

Hello più semplice modo toocheck se l'account disponga delle autorizzazioni appropriate è tramite il portale di hello. Vedere [Controllare le autorizzazioni necessarie](resource-group-create-service-principal-portal.md#required-permissions).

A questo punto, procedere tooa sezione per l'autenticazione con:

* [password](#create-service-principal-with-password)
* [Certificato autofirmato](#create-service-principal-with-self-signed-certificate)
* [Certificato di autorità di certificazione](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>Comandi di PowerShell

tooset di un'entità servizio, utilizzare:

| Comando | Descrizione |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Crea un'entità servizio di Azure Active Directory |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Assegna hello specificato entità di protezione specificata RBAC ruolo toohello, hello specificati ambito. |


## <a name="create-service-principal-with-password"></a>Creare un'entità servizio con password

toocreate un'entità di servizio con il ruolo di collaboratore hello per la sottoscrizione, utilizzare: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

esempio Hello rimane inattivo per tooallow 20 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."

Hello lo script seguente consente di toospecify un ambito diverso da sottoscrizione predefinita hello e tentativi hello assegnazione di ruolo se si verifica un errore:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Alcuni toonote di elementi sullo script hello:

* toogrant hello identità accesso toohello sottoscrizione predefinita, non è necessario tooprovide i parametri di tipo gruppo di risorse o SubscriptionId.
* Specificare il parametro gruppo di risorse hello solo quando si desidera toolimit hello ambito del gruppo di risorse tooa assegnazione ruolo hello.
*  In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello. Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).
* script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."
* Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.


### <a name="provide-credentials-through-powershell"></a>Fornire le credenziali tramite PowerShell
A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello. Nome utente di hello, utilizzare hello `ApplicationId` creato per un'applicazione hello. La password di hello, utilizzare hello quello specificato durante la creazione di account hello. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

ID tenant Hello non è sensibile, pertanto è possibile incorporarlo direttamente nello script. Se è necessario l'ID tenant hello tooretrieve, utilizzare:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Creare un'entità servizio con certificato autofirmato

toocreate un'entità di servizio con un certificato autofirmato e il ruolo di collaboratore hello per la sottoscrizione, utilizzare: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

esempio Hello rimane inattivo per tooallow 20 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."

Hello lo script seguente consente di toospecify un ambito diverso da sottoscrizione predefinita hello e tentativi hello assegnazione di ruolo se si verifica un errore. È necessario che sia installato Azure PowerShell 2.0 su Windows 10 o Windows Server 2016.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Alcuni toonote di elementi sullo script hello:

* toogrant hello identità accesso toohello sottoscrizione predefinita, non è necessario tooprovide i parametri di tipo gruppo di risorse o SubscriptionId.
* Specificare il parametro gruppo di risorse hello solo quando si desidera toolimit hello ambito del gruppo di risorse tooa assegnazione ruolo hello.
* In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello. Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).
* script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."
* Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.

Se si **non dispone di Windows 10 o Windows Server 2016 Technical Preview**, è necessario hello toodownload [generatore certificato autofirmato](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da Microsoft Script Center. Estrarre il contenuto e importare i cmdlet di hello che è necessario.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
Nello script hello, sostituire hello seguenti due certificati di hello toogenerate righe.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Fornire il certificato tramite uno script di PowerShell automatizzato
Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory. Un tenant è un'istanza di Azure Active Directory. Se è disponibile solo una sottoscrizione, è possibile usare:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

un'applicazione Hello ID e l'ID tenant non sono sensibili, pertanto è possibile incorporarli direttamente nello script. Se è necessario l'ID tenant hello tooretrieve, utilizzare:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Se è necessario l'ID dell'applicazione hello tooretrieve, utilizzare:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Creare un'entità servizio con certificato dell'autorità di certificazione
toouse un certificato emesso da un'entità servizio toocreate autorità di certificazione, hello utilizzare lo script seguente:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Alcuni toonote di elementi sullo script hello:

* L'accesso è sottoscrizione toohello con ambito.
* In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello. Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).
* script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory. Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."
* Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.

### <a name="provide-certificate-through-automated-powershell-script"></a>Fornire il certificato tramite uno script di PowerShell automatizzato
Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory. Un tenant è un'istanza di Azure Active Directory.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

un'applicazione Hello ID e l'ID tenant non sono sensibili, pertanto è possibile incorporarli direttamente nello script. Se è necessario l'ID tenant hello tooretrieve, utilizzare:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Se è necessario l'ID dell'applicazione hello tooretrieve, utilizzare:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Modificare le credenziali

le credenziali di hello toochange per un'app di Active Directory, a causa una compromissione della sicurezza o di una scadenza delle credenziali, utilizzano hello [Remove AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [New AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet.

tooremove tutte le credenziali di hello per un'applicazione, utilizzare:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd una password, utilizzare:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd un valore del certificato, creare un certificato autofirmato, come illustrato in questo argomento. Successivamente, usare:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Salvare Accedi toosimplify token di accesso
tooavoid specifica hello servizio principale delle credenziali ogni volta che è necessario toolog in, è possibile salvare il token di accesso di hello.

toouse hello corrente token di accesso in una sessione successiva, salvare il profilo di hello.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Aprire il profilo di hello ed esaminare il relativo contenuto. Si noti che contiene un token di accesso. Anziché manualmente accedere di nuovo, caricare semplicemente il profilo di hello.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> token di accesso Hello scade, usando un profilo salvato funziona solo per purché hello token è valido.
>  

In alternativa, è possibile richiamare le operazioni REST da PowerShell toolog in. Dalla risposta di autenticazione hello, è possibile recuperare il token di accesso hello per l'utilizzo con altre operazioni. Per un esempio di recupero dei token di accesso hello richiamando operazioni REST, vedere [la generazione di un Token di accesso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Debug

È possibile riscontrare hello gli errori seguenti durante la creazione di un'entità servizio:

* **"Authentication_Unauthorized"** o **"alcuna sottoscrizione non trovato nel contesto di hello".** -Viene visualizzato questo errore quando l'account non dispone di hello [delle autorizzazioni necessarie](#required-permissions) su hello Azure Active Directory tooregister un'app. In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore. Chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.

* L'account **"ha azione tooperform autorizzazione 'Microsoft.Authorization/roleAssignments/write' su"sottoscrizioni / {guid}"ambito". ** -Questo errore viene visualizzato quando l'account non dispone di sufficienti autorizzazioni tooassign un'identità tooan ruolo. Chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore.

## <a name="sample-applications"></a>Applicazioni di esempio
Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).
* Per una spiegazione più dettagliata delle applicazioni e delle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md). 
* Per altre informazioni sull'autenticazione di Azure Active Directory, vedere [Scenari di autenticazione per Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).

