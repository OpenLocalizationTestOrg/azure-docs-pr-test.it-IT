---
title: Crittografare i dischi di una macchina virtuale Windows in Azure | Microsoft Docs
description: Come crittografare i dischi virtuali in una VM di Windows per una maggiore sicurezza tramite Azure PowerShell
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
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="c2ea6-103">Come crittografare i dischi virtuali in una VM di Windows</span><span class="sxs-lookup"><span data-stu-id="c2ea6-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="c2ea6-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="c2ea6-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c2ea6-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c2ea6-107">Questo articolo descrive come crittografare i dischi virtuali in una VM di Windows tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="c2ea6-108">È inoltre possibile [crittografare una VM di Linux usando l'interfaccia della riga di comando di Azure 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c2ea6-109">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-109">Overview of disk encryption</span></span>
<span data-ttu-id="c2ea6-110">I dischi virtuali delle VM di Windows vengono crittografati a riposo mediante Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="c2ea6-111">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c2ea6-112">Le chiavi di crittografia vengono archiviate nell'insieme di credenziali delle chiavi di Azure che usano la protezione del software oppure è possibile importare o generare le chiavi in moduli di protezione hardware certificati per gli standard FIPS 140-2 di livello 2.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c2ea6-113">Queste chiavi di crittografia vengono usate per crittografare e decrittografare i dischi virtuali collegati alla VM.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="c2ea6-114">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c2ea6-115">Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c2ea6-116">Il processo per la crittografia di una VM si articola nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c2ea6-117">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c2ea6-118">Configurare la chiave di crittografia in modo da renderla utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="c2ea6-119">Per leggere la chiave di crittografia dall'insieme di credenziali delle chiavi di Azure, creare un'entità servizio di Azure Active Directory con le autorizzazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="c2ea6-120">Eseguire il comando per crittografare i dischi virtuali, specificando l'entità servizio di Azure Active Directory e la chiave di crittografia appropriata da usare.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="c2ea6-121">L'entità servizio di Azure Active Directory richiede la chiave di crittografia necessaria dall'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c2ea6-122">I dischi virtuali vengono crittografati tramite la chiave di crittografia fornita.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="c2ea6-123">Processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="c2ea6-123">Encryption process</span></span>
<span data-ttu-id="c2ea6-124">La crittografia del disco si basa sui componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="c2ea6-125">**Insieme di credenziali delle chiavi di Azure**, che consente di proteggere le chiavi crittografiche e private usate per il processo di crittografia/decrittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="c2ea6-126">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c2ea6-127">Non è necessario dedicare un insieme di credenziali delle chiavi alla crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="c2ea6-128">Per separare i limiti amministrativi e la visibilità delle chiavi, è possibile creare un insieme di credenziali delle chiavi dedicato.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c2ea6-129">**Azure Active Directory** gestisce lo scambio protetto delle chiavi di crittografia necessarie e dell'autenticazione per le azioni richieste.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="c2ea6-130">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="c2ea6-131">L'entità servizio offre un meccanismo protetto per richiedere e consentire il rilascio delle chiavi di crittografia appropriate.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="c2ea6-132">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c2ea6-133">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="c2ea6-133">Requirements and limitations</span></span>
<span data-ttu-id="c2ea6-134">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c2ea6-135">Abilitazione della crittografia in nuove macchine virtuali di Windows da immagini di Azure Marketplace o da un'immagine del disco rigido virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="c2ea6-136">Abilitazione della crittografia nelle macchine virtuali esistenti di Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="c2ea6-137">Abilitazione della crittografia nelle macchine virtuali di Windows configurate usando spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="c2ea6-138">Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="c2ea6-139">Tutte le risorse, come l'insieme di credenziali delle chiavi, l'account di archiviazione e la VM, devono risiedere nella stessa area e nella stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="c2ea6-140">Macchine virtuali di livello standard, ad esempio macchine virtuali di serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c2ea6-141">La crittografia del disco non è attualmente supportata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="c2ea6-142">VM di base.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-142">Basic tier VMs.</span></span>
* <span data-ttu-id="c2ea6-143">VM create con il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="c2ea6-144">Aggiornare le chiavi di crittografia in una VM già crittografata.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="c2ea6-145">Integrazione con il Servizio di gestione delle chiavi locale.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="c2ea6-146">Creare le chiavi e l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="c2ea6-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="c2ea6-147">Prima di iniziare verificare che sia installata la versione più recente del modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="c2ea6-148">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c2ea6-149">Negli esempi di comandi sostituire tutti i parametri di esempio con i propri valori di nome, percorso e chiave.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="c2ea6-150">Negli esempi seguenti viene usata una convenzione di *myResourceGroup*, *myKeyVault*, *myVM* e così via.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="c2ea6-151">Il primo passaggio consiste nel creare un insieme di credenziali delle chiavi di Azure in cui archiviare le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="c2ea6-152">L'insieme di credenziali delle chiavi di Azure consente di archiviare chiavi, chiavi private o password da implementare in tutta sicurezza in applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="c2ea6-153">Per la crittografia del disco virtuale, creare il Key Vault per archiviare una chiave di crittografia usata per crittografare o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="c2ea6-154">Abilitare il provider di Azure Key Vault nella sottoscrizione di Azure con [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) e creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c2ea6-155">L'esempio seguente crea un nome del gruppo di risorse *myResourceGroup* nella posizione *Stati Uniti Orientali*:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="c2ea6-156">L'insieme di credenziali delle chiavi di Azure contenente le chiavi di crittografia e le risorse di calcolo associate, come l'archiviazione e la VM stessa, devono risiedere nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="c2ea6-157">Creare un Azure Key Vault con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e abilitare il Key Vault per l'uso con la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="c2ea6-158">Specificare un nome univoco di Key Vault per *keyVaultName* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="c2ea6-159">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c2ea6-160">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c2ea6-161">Esiste un costo aggiuntivo per creare un insieme di credenziali delle chiavi premium, anziché standard, in cui archiviare le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c2ea6-162">Per creare un Key Vault premium, aggiungere i parametri *-Sku "Premium"* nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="c2ea6-163">L'esempio seguente usa chiavi protette tramite software, poiché viene creato un insieme di credenziali delle chiavi standard.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="c2ea6-164">Per entrambi i modelli di protezione, è necessario consentire alla piattaforma Azure di accedere all'avvio della VM per richiedere le chiavi di crittografia con cui decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="c2ea6-165">Creare una chiave crittografica in Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="c2ea6-166">Nell'esempio seguente viene creata una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="c2ea6-167">Creare un'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2ea6-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="c2ea6-168">Al momento di crittografare o decrittografare i dischi virtuali, specificare un account per gestisce l'autenticazione e lo scambio delle chiavi di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c2ea6-169">Tale account, un'entità servizio di Azure Active Directory, consente alla piattaforma Azure di richiedere le chiavi di crittografia appropriate per conto della VM.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="c2ea6-170">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c2ea6-171">Creare un'entità servizio in Azure Active Directory con [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="c2ea6-172">Per specificare una password sicura seguire [Restrizioni e criteri password in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="c2ea6-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="c2ea6-173">Per crittografare o decrittografare correttamente i dischi virtuali, le autorizzazioni per la chiave di crittografia archiviata nell'insieme di credenziali delle chiavi devono essere impostate in modo tale da consentire all'entità servizio di Azure Active Directory di leggere le chiavi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="c2ea6-174">Impostare le autorizzazioni per Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="c2ea6-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="c2ea6-175">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c2ea6-175">Create virtual machine</span></span>
<span data-ttu-id="c2ea6-176">Per testare il processo di crittografia è necessario creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="c2ea6-177">Nell'esempio seguente viene creata una VM denominata *myVM* usando un'immagine di *Windows Server 2016 Datacenter*:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="c2ea6-178">Crittografare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c2ea6-178">Encrypt virtual machine</span></span>
<span data-ttu-id="c2ea6-179">Per crittografare i dischi virtuali, è necessario riunire tutti i componenti precedenti:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="c2ea6-180">Specificare un'entità servizio e la password di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="c2ea6-181">Specificare l'insieme di credenziali delle chiavi in cui memorizzare i metadati dei dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c2ea6-182">Specificare le chiavi di crittografia da usare per la crittografia e la decrittografia effettive.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="c2ea6-183">Specificare se si desidera crittografare il disco del sistema operativo, i dischi dati o tutti i dischi.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="c2ea6-184">Crittografare la macchina virtuale con [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) tramite la chiave di Azure Key Vault e le credenziali dell'entità servizio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="c2ea6-185">Nell'esempio seguente vengono recuperate tutte le principali informazioni e quindi viene crittografata la macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

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

<span data-ttu-id="c2ea6-186">Accettare la richiesta di continuare la crittografia della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="c2ea6-187">Durante questo processo, la VM viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-187">The VM restarts during the process.</span></span> <span data-ttu-id="c2ea6-188">Dopo aver completato il processo di crittografia e aver riavviato la macchina virtuale, controllare lo stato di crittografia con [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="c2ea6-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="c2ea6-189">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c2ea6-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="c2ea6-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-190">Next steps</span></span>
* <span data-ttu-id="c2ea6-191">Per altre informazioni sulla gestione di Azure Key Vault, vedere [Configurare il Key Vault per le macchine virtuali](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="c2ea6-192">Per altre informazioni sulla crittografia del disco, tra cui come preparare una VM personalizzata con crittografia da caricare in Azure, vedere [Crittografia dischi di Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
