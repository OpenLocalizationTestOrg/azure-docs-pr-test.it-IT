---
title: aaaEncrypt dischi in una macchina virtuale Windows in Azure | Documenti Microsoft
description: "Con Azure PowerShell di protezione avanzata di tooencrypt dischi virtuali in una macchina virtuale di Windows per la modalità"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="01c35-103">Come tooencrypt dischi virtuali in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="01c35-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="01c35-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati.</span><span class="sxs-lookup"><span data-stu-id="01c35-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="01c35-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="01c35-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="01c35-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="01c35-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="01c35-107">Questo articolo dettagli come i dischi virtuali tooencrypt in una macchina virtuale Windows usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01c35-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="01c35-108">È anche possibile [crittografare una VM Linux di hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="01c35-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="01c35-109">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="01c35-109">Overview of disk encryption</span></span>
<span data-ttu-id="01c35-110">I dischi virtuali delle VM di Windows vengono crittografati a riposo mediante Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="01c35-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="01c35-111">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="01c35-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="01c35-112">Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2.</span><span class="sxs-lookup"><span data-stu-id="01c35-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="01c35-113">Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="01c35-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="01c35-114">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="01c35-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="01c35-115">Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="01c35-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="01c35-116">il processo di Hello per la crittografia di una macchina virtuale è il seguente:</span><span class="sxs-lookup"><span data-stu-id="01c35-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="01c35-117">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="01c35-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="01c35-118">Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="01c35-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="01c35-119">chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un servizio di Azure Active Directory principale con le autorizzazioni appropriate di hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="01c35-120">Eseguire hello comando tooencrypt i dischi virtuali, specifica dell'entità servizio di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.</span><span class="sxs-lookup"><span data-stu-id="01c35-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="01c35-121">le entità richieste di servizio Azure Active Directory Hello hello chiave di crittografia richiesto dall'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="01c35-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="01c35-122">i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.</span><span class="sxs-lookup"><span data-stu-id="01c35-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="01c35-123">Processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="01c35-123">Encryption process</span></span>
<span data-ttu-id="01c35-124">Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="01c35-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="01c35-125">**Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco.</span><span class="sxs-lookup"><span data-stu-id="01c35-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="01c35-126">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="01c35-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="01c35-127">Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="01c35-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="01c35-128">limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.</span><span class="sxs-lookup"><span data-stu-id="01c35-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="01c35-129">**Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni.</span><span class="sxs-lookup"><span data-stu-id="01c35-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="01c35-130">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01c35-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="01c35-131">entità servizio Hello fornisce un meccanismo protetto di toorequest e generato le chiavi di crittografia appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="01c35-132">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01c35-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="01c35-133">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="01c35-133">Requirements and limitations</span></span>
<span data-ttu-id="01c35-134">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="01c35-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="01c35-135">Abilitazione della crittografia in nuove macchine virtuali di Windows da immagini di Azure Marketplace o da un'immagine del disco rigido virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="01c35-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="01c35-136">Abilitazione della crittografia nelle macchine virtuali esistenti di Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="01c35-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="01c35-137">Abilitazione della crittografia nelle macchine virtuali di Windows configurate usando spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="01c35-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="01c35-138">Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="01c35-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="01c35-139">Tutte le risorse (ad esempio l'insieme di credenziali chiave, l'account di archiviazione e macchina virtuale) devono essere in hello stessa regione di Azure e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="01c35-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="01c35-140">Macchine virtuali di livello standard, ad esempio macchine virtuali di serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="01c35-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="01c35-141">Crittografia del disco non è attualmente supportata nei seguenti scenari hello:</span><span class="sxs-lookup"><span data-stu-id="01c35-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="01c35-142">VM di base.</span><span class="sxs-lookup"><span data-stu-id="01c35-142">Basic tier VMs.</span></span>
* <span data-ttu-id="01c35-143">Macchine virtuali create con modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="01c35-144">Aggiornamento delle chiavi di crittografia in una VM già crittografata hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="01c35-145">Integrazione con il Servizio di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="01c35-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="01c35-146">Creare le chiavi e l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="01c35-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="01c35-147">Prima di iniziare, verificare che la versione più recente di hello di hello Azure PowerShell modulo è stato installato.</span><span class="sxs-lookup"><span data-stu-id="01c35-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="01c35-148">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01c35-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="01c35-149">Nel corso di esempi di comandi hello, sostituire tutti i parametri di esempio con i nomi, percorso e i valori di chiave.</span><span class="sxs-lookup"><span data-stu-id="01c35-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="01c35-150">Negli esempi seguenti Hello utilizzano una convenzione di *myResourceGroup*, *myKeyVault*, *myVM*e così via.</span><span class="sxs-lookup"><span data-stu-id="01c35-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="01c35-151">primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="01c35-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="01c35-152">Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="01c35-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="01c35-153">Per la crittografia del disco virtuale, si crea un insieme di credenziali chiave di toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="01c35-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="01c35-154">Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure con [registro AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), quindi creare un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="01c35-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="01c35-155">esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello *Stati Uniti orientali* percorso:</span><span class="sxs-lookup"><span data-stu-id="01c35-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="01c35-156">Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="01c35-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="01c35-157">Creare un insieme di credenziali chiave di Azure con [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="01c35-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="01c35-158">Specificare un nome univoco di Key Vault per *keyVaultName* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01c35-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="01c35-159">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="01c35-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="01c35-160">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="01c35-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="01c35-161">È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="01c35-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="01c35-162">un insieme di credenziali chiave premium nel precedente passaggio hello toocreate aggiungere hello *- Sku "Premium"* parametri.</span><span class="sxs-lookup"><span data-stu-id="01c35-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="01c35-163">Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard.</span><span class="sxs-lookup"><span data-stu-id="01c35-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="01c35-164">Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="01c35-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="01c35-165">Creare una chiave crittografica in Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="01c35-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="01c35-166">esempio Hello crea una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="01c35-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="01c35-167">Creare hello dell'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01c35-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="01c35-168">Quando i dischi virtuali vengono crittografati o decrittografati, specificare l'autenticazione di account toohandle hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="01c35-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="01c35-169">Questo account, un'entità di servizio di Azure Active Directory consente hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="01c35-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="01c35-170">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="01c35-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="01c35-171">Creare un'entità servizio in Azure Active Directory con [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="01c35-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="01c35-172">toospecify una password sicura, seguire hello [restrizioni in Azure Active Directory e criteri Password](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="01c35-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="01c35-173">toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere principale tooread hello chiavi del set toopermit hello Azure Active Directory del servizio.</span><span class="sxs-lookup"><span data-stu-id="01c35-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="01c35-174">Impostare le autorizzazioni per Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="01c35-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="01c35-175">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="01c35-175">Create virtual machine</span></span>
<span data-ttu-id="01c35-176">tootest hello processo di crittografia, creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="01c35-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="01c35-177">esempio Hello crea una macchina virtuale denominata *myVM* utilizzando un *Data Center di Windows Server 2016* immagine:</span><span class="sxs-lookup"><span data-stu-id="01c35-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="01c35-178">Crittografare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="01c35-178">Encrypt virtual machine</span></span>
<span data-ttu-id="01c35-179">tooencrypt hello i dischi virtuali, riunire tutti i componenti precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="01c35-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="01c35-180">Specificare hello entità servizio di Azure Active Directory e una password.</span><span class="sxs-lookup"><span data-stu-id="01c35-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="01c35-181">Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="01c35-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="01c35-182">Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.</span><span class="sxs-lookup"><span data-stu-id="01c35-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="01c35-183">Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.</span><span class="sxs-lookup"><span data-stu-id="01c35-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="01c35-184">Crittografare la macchina virtuale con [Set AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) utilizzando la chiave di insieme credenziali chiavi Azure hello e le credenziali dell'entità servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01c35-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="01c35-185">Recupera tutte le informazioni chiave hello Hello esempio seguente viene quindi crittografa hello macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="01c35-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="01c35-186">Accettare hello toocontinue prompt dei comandi con la crittografia di VM hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="01c35-187">Hello VM viene riavviato durante il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="01c35-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="01c35-188">Una volta completato il processo di crittografia hello e hello VM è stato riavviato, verificare lo stato di crittografia hello con [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="01c35-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="01c35-189">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="01c35-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="01c35-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01c35-190">Next steps</span></span>
* <span data-ttu-id="01c35-191">Per altre informazioni sulla gestione di Azure Key Vault, vedere [Configurare il Key Vault per le macchine virtuali](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="01c35-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="01c35-192">Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="01c35-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
