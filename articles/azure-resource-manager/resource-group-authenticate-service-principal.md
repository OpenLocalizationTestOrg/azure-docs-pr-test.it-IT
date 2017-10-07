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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="27e0f-104">Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="27e0f-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="27e0f-105">Quando si dispone di un'app o script che richiede risorse tooaccess, è possibile impostare un'identità per l'applicazione hello e l'applicazione hello con le proprie credenziali di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="27e0f-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="27e0f-106">Questa identità è nota come entità servizio.</span><span class="sxs-lookup"><span data-stu-id="27e0f-106">This identity is known as a service principal.</span></span> <span data-ttu-id="27e0f-107">Questo approccio consente di:</span><span class="sxs-lookup"><span data-stu-id="27e0f-107">This approach enables you to:</span></span>

* <span data-ttu-id="27e0f-108">Assegnare le autorizzazioni di identità app toohello che sono diverse dalle proprie autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="27e0f-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="27e0f-109">In genere, queste autorizzazioni sono limitate tooexactly quali app hello deve toodo.</span><span class="sxs-lookup"><span data-stu-id="27e0f-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="27e0f-110">Usare un certificato per l'autenticazione in caso di esecuzione di uno script automatico.</span><span class="sxs-lookup"><span data-stu-id="27e0f-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="27e0f-111">In questo argomento illustra come toouse [Azure PowerShell](/powershell/azure/overview) tooset le operazioni necessarie per un'applicazione toorun sotto le proprie credenziali e l'identità.</span><span class="sxs-lookup"><span data-stu-id="27e0f-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="27e0f-112">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="27e0f-112">Required permissions</span></span>
<span data-ttu-id="27e0f-113">toocomplete in questo argomento, è necessario disporre delle autorizzazioni sufficienti in Azure Active Directory sia la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="27e0f-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="27e0f-114">In particolare, devono essere in grado di toocreate un'app in Azure Active Directory hello e assegnazione di ruolo tooa principale di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="27e0f-115">Hello più semplice modo toocheck se l'account disponga delle autorizzazioni appropriate è tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="27e0f-116">Vedere [Controllare le autorizzazioni necessarie](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="27e0f-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="27e0f-117">A questo punto, procedere tooa sezione per l'autenticazione con:</span><span class="sxs-lookup"><span data-stu-id="27e0f-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="27e0f-118">password</span><span class="sxs-lookup"><span data-stu-id="27e0f-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="27e0f-119">Certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="27e0f-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="27e0f-120">Certificato di autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="27e0f-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="27e0f-121">Comandi di PowerShell</span><span class="sxs-lookup"><span data-stu-id="27e0f-121">PowerShell commands</span></span>

<span data-ttu-id="27e0f-122">tooset di un'entità servizio, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="27e0f-123">Comando</span><span class="sxs-lookup"><span data-stu-id="27e0f-123">Command</span></span> | <span data-ttu-id="27e0f-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="27e0f-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="27e0f-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="27e0f-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="27e0f-126">Crea un'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27e0f-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="27e0f-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="27e0f-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="27e0f-128">Assegna hello specificato entità di protezione specificata RBAC ruolo toohello, hello specificati ambito.</span><span class="sxs-lookup"><span data-stu-id="27e0f-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="27e0f-129">Creare un'entità servizio con password</span><span class="sxs-lookup"><span data-stu-id="27e0f-129">Create service principal with password</span></span>

<span data-ttu-id="27e0f-130">toocreate un'entità di servizio con il ruolo di collaboratore hello per la sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="27e0f-131">esempio Hello rimane inattivo per tooallow 20 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27e0f-132">Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."</span><span class="sxs-lookup"><span data-stu-id="27e0f-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="27e0f-133">Hello lo script seguente consente di toospecify un ambito diverso da sottoscrizione predefinita hello e tentativi hello assegnazione di ruolo se si verifica un errore:</span><span class="sxs-lookup"><span data-stu-id="27e0f-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="27e0f-134">Alcuni toonote di elementi sullo script hello:</span><span class="sxs-lookup"><span data-stu-id="27e0f-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="27e0f-135">toogrant hello identità accesso toohello sottoscrizione predefinita, non è necessario tooprovide i parametri di tipo gruppo di risorse o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="27e0f-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="27e0f-136">Specificare il parametro gruppo di risorse hello solo quando si desidera toolimit hello ambito del gruppo di risorse tooa assegnazione ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="27e0f-137">In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="27e0f-138">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="27e0f-139">script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27e0f-140">Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."</span><span class="sxs-lookup"><span data-stu-id="27e0f-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="27e0f-141">Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="27e0f-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="27e0f-142">Fornire le credenziali tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="27e0f-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="27e0f-143">A questo punto, è necessario toolog in come operazioni tooperform dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="27e0f-144">Nome utente di hello, utilizzare hello `ApplicationId` creato per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="27e0f-145">La password di hello, utilizzare hello quello specificato durante la creazione di account hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="27e0f-146">ID tenant Hello non è sensibile, pertanto è possibile incorporarlo direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="27e0f-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="27e0f-147">Se è necessario l'ID tenant hello tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="27e0f-148">Creare un'entità servizio con certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="27e0f-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="27e0f-149">toocreate un'entità di servizio con un certificato autofirmato e il ruolo di collaboratore hello per la sottoscrizione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="27e0f-150">esempio Hello rimane inattivo per tooallow 20 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27e0f-151">Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."</span><span class="sxs-lookup"><span data-stu-id="27e0f-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="27e0f-152">Hello lo script seguente consente di toospecify un ambito diverso da sottoscrizione predefinita hello e tentativi hello assegnazione di ruolo se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="27e0f-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="27e0f-153">È necessario che sia installato Azure PowerShell 2.0 su Windows 10 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="27e0f-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="27e0f-154">Alcuni toonote di elementi sullo script hello:</span><span class="sxs-lookup"><span data-stu-id="27e0f-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="27e0f-155">toogrant hello identità accesso toohello sottoscrizione predefinita, non è necessario tooprovide i parametri di tipo gruppo di risorse o SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="27e0f-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="27e0f-156">Specificare il parametro gruppo di risorse hello solo quando si desidera toolimit hello ambito del gruppo di risorse tooa assegnazione ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="27e0f-157">In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="27e0f-158">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="27e0f-159">script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27e0f-160">Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."</span><span class="sxs-lookup"><span data-stu-id="27e0f-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="27e0f-161">Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="27e0f-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="27e0f-162">Se si **non dispone di Windows 10 o Windows Server 2016 Technical Preview**, è necessario hello toodownload [generatore certificato autofirmato](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="27e0f-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="27e0f-163">Estrarre il contenuto e importare i cmdlet di hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="27e0f-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="27e0f-164">Nello script hello, sostituire hello seguenti due certificati di hello toogenerate righe.</span><span class="sxs-lookup"><span data-stu-id="27e0f-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="27e0f-165">Fornire il certificato tramite uno script di PowerShell automatizzato</span><span class="sxs-lookup"><span data-stu-id="27e0f-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="27e0f-166">Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="27e0f-167">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="27e0f-168">Se è disponibile solo una sottoscrizione, è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="27e0f-169">un'applicazione Hello ID e l'ID tenant non sono sensibili, pertanto è possibile incorporarli direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="27e0f-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="27e0f-170">Se è necessario l'ID tenant hello tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="27e0f-171">Se è necessario l'ID dell'applicazione hello tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="27e0f-172">Creare un'entità servizio con certificato dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="27e0f-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="27e0f-173">toouse un certificato emesso da un'entità servizio toocreate autorità di certificazione, hello utilizzare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="27e0f-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="27e0f-174">Alcuni toonote di elementi sullo script hello:</span><span class="sxs-lookup"><span data-stu-id="27e0f-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="27e0f-175">L'accesso è sottoscrizione toohello con ambito.</span><span class="sxs-lookup"><span data-stu-id="27e0f-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="27e0f-176">In questo esempio, aggiungere un ruolo Collaboratore toohello dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="27e0f-177">Per gli altri ruoli, vedere [Controllo degli accessi in base al ruolo: ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="27e0f-178">script Hello rimane inattivo per tooallow 15 secondi del tempo hello toopropagate principale nuovo servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27e0f-179">Se lo script non attende tempo sufficiente, è visualizzato un errore indicante: "PrincipalNotFound: entità {id} non esiste nella directory hello."</span><span class="sxs-lookup"><span data-stu-id="27e0f-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="27e0f-180">Se è necessario sottoscrizioni toomore accesso principale di toogrant hello servizio o gruppi di risorse, eseguire hello `New-AzureRMRoleAssignment` nuovamente cmdlet con ambiti diversi.</span><span class="sxs-lookup"><span data-stu-id="27e0f-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="27e0f-181">Fornire il certificato tramite uno script di PowerShell automatizzato</span><span class="sxs-lookup"><span data-stu-id="27e0f-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="27e0f-182">Ogni volta che si accede come un'entità servizio, è necessario id tenant di hello tooprovide della directory hello per le app di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="27e0f-183">Un tenant è un'istanza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27e0f-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="27e0f-184">un'applicazione Hello ID e l'ID tenant non sono sensibili, pertanto è possibile incorporarli direttamente nello script.</span><span class="sxs-lookup"><span data-stu-id="27e0f-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="27e0f-185">Se è necessario l'ID tenant hello tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="27e0f-186">Se è necessario l'ID dell'applicazione hello tooretrieve, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="27e0f-187">Modificare le credenziali</span><span class="sxs-lookup"><span data-stu-id="27e0f-187">Change credentials</span></span>

<span data-ttu-id="27e0f-188">le credenziali di hello toochange per un'app di Active Directory, a causa una compromissione della sicurezza o di una scadenza delle credenziali, utilizzano hello [Remove AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) e [New AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27e0f-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="27e0f-189">tooremove tutte le credenziali di hello per un'applicazione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="27e0f-190">tooadd una password, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="27e0f-191">tooadd un valore del certificato, creare un certificato autofirmato, come illustrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="27e0f-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="27e0f-192">Successivamente, usare:</span><span class="sxs-lookup"><span data-stu-id="27e0f-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="27e0f-193">Salvare Accedi toosimplify token di accesso</span><span class="sxs-lookup"><span data-stu-id="27e0f-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="27e0f-194">tooavoid specifica hello servizio principale delle credenziali ogni volta che è necessario toolog in, è possibile salvare il token di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="27e0f-195">toouse hello corrente token di accesso in una sessione successiva, salvare il profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="27e0f-196">Aprire il profilo di hello ed esaminare il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="27e0f-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="27e0f-197">Si noti che contiene un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="27e0f-197">Notice that it contains an access token.</span></span> <span data-ttu-id="27e0f-198">Anziché manualmente accedere di nuovo, caricare semplicemente il profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="27e0f-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="27e0f-199">token di accesso Hello scade, usando un profilo salvato funziona solo per purché hello token è valido.</span><span class="sxs-lookup"><span data-stu-id="27e0f-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="27e0f-200">In alternativa, è possibile richiamare le operazioni REST da PowerShell toolog in.</span><span class="sxs-lookup"><span data-stu-id="27e0f-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="27e0f-201">Dalla risposta di autenticazione hello, è possibile recuperare il token di accesso hello per l'utilizzo con altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="27e0f-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="27e0f-202">Per un esempio di recupero dei token di accesso hello richiamando operazioni REST, vedere [la generazione di un Token di accesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="27e0f-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="27e0f-203">Debug</span><span class="sxs-lookup"><span data-stu-id="27e0f-203">Debug</span></span>

<span data-ttu-id="27e0f-204">È possibile riscontrare hello gli errori seguenti durante la creazione di un'entità servizio:</span><span class="sxs-lookup"><span data-stu-id="27e0f-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="27e0f-205">**"Authentication_Unauthorized"** o **"alcuna sottoscrizione non trovato nel contesto di hello".**</span><span class="sxs-lookup"><span data-stu-id="27e0f-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="27e0f-206">-Viene visualizzato questo errore quando l'account non dispone di hello [delle autorizzazioni necessarie](#required-permissions) su hello Azure Active Directory tooregister un'app.</span><span class="sxs-lookup"><span data-stu-id="27e0f-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="27e0f-207">In genere, l'errore si verifica quando solo gli utenti amministratori di Azure Active Directory possono registrare le app e l'account in uso non è un account di amministratore. Chiedere tooeither l'amministratore assegna si tooan ruolo di amministratore o tooenable utenti tooregister app.</span><span class="sxs-lookup"><span data-stu-id="27e0f-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="27e0f-208">L'account **"ha azione tooperform autorizzazione 'Microsoft.Authorization/roleAssignments/write' su"sottoscrizioni / {guid}"ambito". ** -Questo errore viene visualizzato quando l'account non dispone di sufficienti autorizzazioni tooassign un'identità tooan ruolo.</span><span class="sxs-lookup"><span data-stu-id="27e0f-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="27e0f-209">Chiedere il tooadd amministratore sottoscrizione si tooUser accesso ruolo di amministratore.</span><span class="sxs-lookup"><span data-stu-id="27e0f-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="27e0f-210">Applicazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="27e0f-210">Sample applications</span></span>
<span data-ttu-id="27e0f-211">Per informazioni su come un'applicazione hello tramite diverse piattaforme, vedere:</span><span class="sxs-lookup"><span data-stu-id="27e0f-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="27e0f-212">.NET</span><span class="sxs-lookup"><span data-stu-id="27e0f-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="27e0f-213">Java</span><span class="sxs-lookup"><span data-stu-id="27e0f-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="27e0f-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="27e0f-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="27e0f-215">Python</span><span class="sxs-lookup"><span data-stu-id="27e0f-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="27e0f-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="27e0f-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="27e0f-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27e0f-217">Next steps</span></span>
* <span data-ttu-id="27e0f-218">Per informazioni dettagliate sull'integrazione di un'applicazione in Azure per la gestione delle risorse, vedere [tooauthorization di Guida per gli sviluppatori con API di gestione risorse di Azure hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="27e0f-219">Per una spiegazione più dettagliata delle applicazioni e delle entità servizio, vedere [Oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="27e0f-220">Per altre informazioni sull'autenticazione di Azure Active Directory, vedere [Scenari di autenticazione per Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="27e0f-221">Per un elenco di azioni disponibili che possono essere concesse o negate toousers, vedere [operazioni di Provider di risorse di Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="27e0f-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

