---
title: "Creare un'identità per un'app Azure con PowerShell | Documentazione Microsoft"
description: "Descrive come usare Azure PowerShell per creare un'applicazione Azure Active Directory e un'entità servizio e concedere l'accesso alle risorse tramite il controllo degli accessi in base al ruolo. Illustra come autenticare l'applicazione con una password o un certificato."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="a4fad-104">Usare Azure PowerShell per creare un'entità servizio per accedere alle risorse</span><span class="sxs-lookup"><span data-stu-id="a4fad-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="a4fad-105">Quando si ha un'app o uno script che deve accedere alle risorse, è possibile configurare un'identità per l'app ed eseguirne l'autenticazione con credenziali specifiche.</span><span class="sxs-lookup"><span data-stu-id="a4fad-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="a4fad-106">Questa identità è nota come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="a4fad-106">This identity is known as a service principal.</span></span> <span data-ttu-id="a4fad-107">Questo approccio consente di:</span><span class="sxs-lookup"><span data-stu-id="a4fad-107">This approach enables you to:</span></span>

* <span data-ttu-id="a4fad-108">Assegnare all'identità dell'app autorizzazioni diverse rispetto a quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a4fad-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="a4fad-109">Tali autorizzazioni sono in genere limitate alle specifiche operazioni che devono essere eseguite dall'app.</span><span class="sxs-lookup"><span data-stu-id="a4fad-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="a4fad-110">Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="a4fad-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="a4fad-111">Questo argomento illustra come usare [Azure PowerShell](/powershell/azure/overview) per impostare tutte le informazioni necessarie a un'applicazione per l'esecuzione con credenziali e identità proprie.</span><span class="sxs-lookup"><span data-stu-id="a4fad-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="a4fad-112">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="a4fad-112">Required permissions</span></span>
<span data-ttu-id="a4fad-113">Per completare questo argomento è necessario avere autorizzazioni sufficienti sia nell'istanza di Azure Active Directory che nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4fad-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="a4fad-114">In particolare, è necessario poter creare un'app in Azure Active Directory e assegnare l'entità servizio a un ruolo.</span><span class="sxs-lookup"><span data-stu-id="a4fad-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="a4fad-115">Il modo più semplice per verificare se l'account dispone delle autorizzazioni appropriate è tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="a4fad-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="a4fad-116">Vedere [Controllare le autorizzazioni necessarie](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="a4fad-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="a4fad-117">A questo punto, procedere a una sezione per l'autenticazione con:</span><span class="sxs-lookup"><span data-stu-id="a4fad-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="a4fad-118">password</span><span class="sxs-lookup"><span data-stu-id="a4fad-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="a4fad-119">Certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="a4fad-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="a4fad-120">Certificato di autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="a4fad-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="a4fad-121">Comandi di PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fad-121">PowerShell commands</span></span>

<span data-ttu-id="a4fad-122">Per configurare un'entità servizio, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="a4fad-123">Comando</span><span class="sxs-lookup"><span data-stu-id="a4fad-123">Command</span></span> | <span data-ttu-id="a4fad-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4fad-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="a4fad-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="a4fad-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="a4fad-126">Crea un'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4fad-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="a4fad-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="a4fad-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="a4fad-128">Assegna il ruolo specificato del controllo degli accessi in base al ruolo all'entità specificata nell'ambito specificato.</span><span class="sxs-lookup"><span data-stu-id="a4fad-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="a4fad-129">Creare un'entità servizio con password</span><span class="sxs-lookup"><span data-stu-id="a4fad-129">Create service principal with password</span></span>

<span data-ttu-id="a4fad-130">Per creare un'entità servizio con il ruolo Collaboratore per la sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="a4fad-131">L'esempio viene sospeso per 20 secondi per consentire la propagazione della nuova entità servizio in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a4fad-132">Se la durata dell'attesa dello script non è sufficiente, viene visualizzato un errore simile al seguente: "PrincipalNotFound: L'entità {id} non esiste nella directory".</span><span class="sxs-lookup"><span data-stu-id="a4fad-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="a4fad-133">Lo script seguente consente di specificare un ambito diverso dalla sottoscrizione predefinita e ritenta l'assegnazione del ruolo, se si verifica un errore:</span><span class="sxs-lookup"><span data-stu-id="a4fad-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="a4fad-134">Alcuni elementi da considerare per lo script:</span><span class="sxs-lookup"><span data-stu-id="a4fad-134">A few items to note about the script:</span></span>

* <span data-ttu-id="a4fad-135">Per concedere l'accesso all'identità alla sottoscrizione predefinita, non è necessario specificare i parametri ResourceGroup o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="a4fad-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="a4fad-136">Specificare il parametro ResourceGroup solo quando si vuole limitare l'ambito dell'assegnazione di ruolo a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4fad-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="a4fad-137">In questo esempio viene aggiunta l'entità servizio al ruolo Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="a4fad-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="a4fad-138">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a4fad-139">Lo script viene sospeso per 15 secondi per consentire la propagazione della nuova entità servizio in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a4fad-140">Se la durata dell'attesa dello script non è sufficiente, viene visualizzato un errore simile al seguente: "PrincipalNotFound: L'entità {id} non esiste nella directory".</span><span class="sxs-lookup"><span data-stu-id="a4fad-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="a4fad-141">Se è necessario concedere l'accesso all'entità servizio a più sottoscrizioni o gruppi di risorse, eseguire il cmdlet `New-AzureRMRoleAssignment` con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="a4fad-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="a4fad-142">Fornire le credenziali tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fad-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="a4fad-143">A questo punto è necessario accedere come applicazione per eseguire operazioni.</span><span class="sxs-lookup"><span data-stu-id="a4fad-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="a4fad-144">Per il nome utente, usare il valore `ApplicationId` creato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4fad-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="a4fad-145">Per la password, usare quella specificata durante la creazione dell'account.</span><span class="sxs-lookup"><span data-stu-id="a4fad-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="a4fad-146">Poiché l'ID tenant non è sensibile, è possibile incorporarlo direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="a4fad-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="a4fad-147">Se è necessario recuperare l'ID tenant, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="a4fad-148">Creare un'entità servizio con certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="a4fad-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="a4fad-149">Per creare un'entità servizio con un certificato autofirmato e il ruolo Collaboratore per la sottoscrizione, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="a4fad-150">L'esempio viene sospeso per 20 secondi per consentire la propagazione della nuova entità servizio in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a4fad-151">Se la durata dell'attesa dello script non è sufficiente, viene visualizzato un errore simile al seguente: "PrincipalNotFound: L'entità {id} non esiste nella directory".</span><span class="sxs-lookup"><span data-stu-id="a4fad-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="a4fad-152">Lo script seguente consente di specificare un ambito diverso dalla sottoscrizione predefinita e ritenta l'assegnazione di ruolo, se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="a4fad-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="a4fad-153">È necessario che sia installato Azure PowerShell 2.0 su Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a4fad-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="a4fad-154">Alcuni elementi da considerare per lo script:</span><span class="sxs-lookup"><span data-stu-id="a4fad-154">A few items to note about the script:</span></span>

* <span data-ttu-id="a4fad-155">Per concedere l'accesso all'identità alla sottoscrizione predefinita, non è necessario specificare i parametri ResourceGroup o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="a4fad-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="a4fad-156">Specificare il parametro ResourceGroup solo quando si vuole limitare l'ambito dell'assegnazione di ruolo a un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4fad-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="a4fad-157">In questo esempio viene aggiunta l'entità servizio al ruolo Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="a4fad-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="a4fad-158">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a4fad-159">Lo script viene sospeso per 15 secondi per consentire la propagazione della nuova entità servizio in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a4fad-160">Se la durata dell'attesa dello script non è sufficiente, viene visualizzato un errore simile al seguente: "PrincipalNotFound: L'entità {id} non esiste nella directory".</span><span class="sxs-lookup"><span data-stu-id="a4fad-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="a4fad-161">Se è necessario concedere l'accesso all'entità servizio a più sottoscrizioni o gruppi di risorse, eseguire il cmdlet `New-AzureRMRoleAssignment` con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="a4fad-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="a4fad-162">Se **non si dispone di Windows 10 o Windows Server 2016 Technical Preview**, è necessario scaricare il [generatore di certificato autofirmato](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="a4fad-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="a4fad-163">Estrarre i contenuti e importare il cmdlet necessario.</span><span class="sxs-lookup"><span data-stu-id="a4fad-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="a4fad-164">Nello script sostituire le due righe seguenti per generare il certificato.</span><span class="sxs-lookup"><span data-stu-id="a4fad-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="a4fad-165">Fornire il certificato tramite uno script di PowerShell automatizzato</span><span class="sxs-lookup"><span data-stu-id="a4fad-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="a4fad-166">Ogni volta che si accede come un'entità servizio, è necessario fornire l'ID tenant della directory per l'app AD.</span><span class="sxs-lookup"><span data-stu-id="a4fad-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="a4fad-167">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="a4fad-168">Se è disponibile solo una sottoscrizione, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="a4fad-169">Poiché l'ID applicazione e l'ID tenant non sono sensibili, è possibile incorporarli direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="a4fad-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="a4fad-170">Se è necessario recuperare l'ID tenant, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="a4fad-171">Se è necessario recuperare l'ID applicazione, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="a4fad-172">Creare un'entità servizio con certificato dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="a4fad-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="a4fad-173">Per usare un certificato emesso da un'autorità di certificazione per creare un'entità servizio, usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="a4fad-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="a4fad-174">Alcuni elementi da considerare per lo script:</span><span class="sxs-lookup"><span data-stu-id="a4fad-174">A few items to note about the script:</span></span>

* <span data-ttu-id="a4fad-175">L'ambito di accesso è limitato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a4fad-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="a4fad-176">In questo esempio viene aggiunta l'entità servizio al ruolo Collaboratore.</span><span class="sxs-lookup"><span data-stu-id="a4fad-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="a4fad-177">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a4fad-178">Lo script viene sospeso per 15 secondi per consentire la propagazione della nuova entità servizio in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a4fad-179">Se la durata dell'attesa dello script non è sufficiente, viene visualizzato un errore simile al seguente: "PrincipalNotFound: L'entità {id} non esiste nella directory".</span><span class="sxs-lookup"><span data-stu-id="a4fad-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="a4fad-180">Se è necessario concedere l'accesso all'entità servizio a più sottoscrizioni o gruppi di risorse, eseguire il cmdlet `New-AzureRMRoleAssignment` con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="a4fad-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="a4fad-181">Fornire il certificato tramite uno script di PowerShell automatizzato</span><span class="sxs-lookup"><span data-stu-id="a4fad-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="a4fad-182">Ogni volta che si accede come un'entità servizio, è necessario fornire l'ID tenant della directory per l'app AD.</span><span class="sxs-lookup"><span data-stu-id="a4fad-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="a4fad-183">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4fad-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="a4fad-184">Poiché l'ID applicazione e l'ID tenant non sono sensibili, è possibile incorporarli direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="a4fad-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="a4fad-185">Se è necessario recuperare l'ID tenant, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="a4fad-186">Se è necessario recuperare l'ID applicazione, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="a4fad-187">Modificare le credenziali</span><span class="sxs-lookup"><span data-stu-id="a4fad-187">Change credentials</span></span>

<span data-ttu-id="a4fad-188">Per modificare le credenziali per un'app AD, a causa di una violazione della sicurezza o della scadenza delle credenziali, usare i cmdlet [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential).</span><span class="sxs-lookup"><span data-stu-id="a4fad-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="a4fad-189">Per rimuovere tutte le credenziali per un'applicazione, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="a4fad-190">Per aggiungere una password, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="a4fad-191">Per aggiungere un valore del certificato, creare un certificato autofirmato come illustrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a4fad-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="a4fad-192">Successivamente, usare:</span><span class="sxs-lookup"><span data-stu-id="a4fad-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="a4fad-193">Salvare il token di accesso per semplificare l'accesso</span><span class="sxs-lookup"><span data-stu-id="a4fad-193">Save access token to simplify log in</span></span>
<span data-ttu-id="a4fad-194">Il token di accesso può essere slavato al fine di evitare di dover fornire le credenziali dell'entità servizio ogni volta che viene richiesto di effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a4fad-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="a4fad-195">Salvare il profilo per usare il token di accesso corrente in una sessione successiva.</span><span class="sxs-lookup"><span data-stu-id="a4fad-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="a4fad-196">Aprire il profilo ed esaminare il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="a4fad-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="a4fad-197">Si noti che contiene un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="a4fad-197">Notice that it contains an access token.</span></span> <span data-ttu-id="a4fad-198">Anziché effettuare di nuovo l'accesso manuale, è sufficiente caricare il profilo.</span><span class="sxs-lookup"><span data-stu-id="a4fad-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="a4fad-199">Il token di accesso scade, quindi l'uso di un profilo salvato funziona solo fino al termine del periodo di validità del token.</span><span class="sxs-lookup"><span data-stu-id="a4fad-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="a4fad-200">In alternativa, è possibile richiamare operazioni REST da PowerShell per eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a4fad-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="a4fad-201">Dalla risposta di autenticazione è possibile recuperare il token di accesso da usare con altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="a4fad-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="a4fad-202">Per un esempio di come recuperare il token di accesso richiamando operazioni REST, vedere [Generazione di un token di accesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="a4fad-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="a4fad-203">Debug</span><span class="sxs-lookup"><span data-stu-id="a4fad-203">Debug</span></span>

<span data-ttu-id="a4fad-204">Durante la creazione di un'entità servizio, è possibile riscontrare gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4fad-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="a4fad-205">**"Authentication_Unauthorized"** o **"Nessuna sottoscrizione trovata nel contesto".**</span><span class="sxs-lookup"><span data-stu-id="a4fad-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="a4fad-206">- Questo errore viene visualizzato quando l'account non ha le [autorizzazioni necessarie](#required-permissions) in Azure Active Directory per registrare un'app.</span><span class="sxs-lookup"><span data-stu-id="a4fad-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="a4fad-207">In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore.</span><span class="sxs-lookup"><span data-stu-id="a4fad-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="a4fad-208">Chiedere all'amministratore di essere assegnati a un ruolo di amministratore oppure di consentire agli utenti di registrare le app.</span><span class="sxs-lookup"><span data-stu-id="a4fad-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="a4fad-209">L'account **"non è autorizzato a eseguire l'azione 'Microsoft.Authorization/roleAssignments/write' nell'ambito '/subscriptions/{guid}'."** - Questo errore viene visualizzato quando l'account non dispone di autorizzazioni sufficienti per assegnare un ruolo a un'identità.</span><span class="sxs-lookup"><span data-stu-id="a4fad-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="a4fad-210">Chiedere all'amministratore della sottoscrizione di essere aggiunti al ruolo Amministratore accessi utente.</span><span class="sxs-lookup"><span data-stu-id="a4fad-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="a4fad-211">Applicazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="a4fad-211">Sample applications</span></span>
<span data-ttu-id="a4fad-212">Per informazioni su come effettuare l'accesso all'applicazione su diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="a4fad-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="a4fad-213">.NET</span><span class="sxs-lookup"><span data-stu-id="a4fad-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="a4fad-214">Java</span><span class="sxs-lookup"><span data-stu-id="a4fad-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="a4fad-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4fad-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="a4fad-216">Python</span><span class="sxs-lookup"><span data-stu-id="a4fad-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="a4fad-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="a4fad-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="a4fad-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4fad-218">Next steps</span></span>
* <span data-ttu-id="a4fad-219">Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [Guida per gli sviluppatori all'autorizzazione con l'API di Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="a4fad-220">Per una spiegazione più dettagliata delle applicazioni e delle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="a4fad-221">Per altre informazioni sull'autenticazione di Azure Active Directory, vedere [Scenari di autenticazione per Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="a4fad-222">Per un elenco di azioni disponibili che è possibile concedere o negare agli utenti, vedere [Operazioni di provider di risorse con Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a4fad-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

