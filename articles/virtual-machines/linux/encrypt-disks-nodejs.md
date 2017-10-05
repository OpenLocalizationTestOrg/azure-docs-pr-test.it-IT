---
title: Crittografare dischi in una macchina virtuale Linux con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Come crittografare i dischi di una macchina virtuale Linux tramite l'interfaccia della riga di comando di Azure 1.0 e il modello di distribuzione di Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="f2ce6-103">Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f2ce6-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="f2ce6-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati a riposo.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="f2ce6-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="f2ce6-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="f2ce6-107">In questo articolo viene spiegato come crittografare i dischi virtuali di una VM Linux tramite l'interfaccia della riga di comando di Azure 1.0 e il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f2ce6-108">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="f2ce6-108">CLI versions to complete the task</span></span>
<span data-ttu-id="f2ce6-109">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f2ce6-110">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="f2ce6-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f2ce6-111">[Interfaccia della riga di comando di Azure 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="f2ce6-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f2ce6-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="f2ce6-112">Quick commands</span></span>
<span data-ttu-id="f2ce6-113">Se si necessita di eseguire rapidamente l'attività, nella sezione seguente sono illustrati i comandi di base per crittografare i dischi rigidi della VM.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="f2ce6-114">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="f2ce6-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="f2ce6-115">È necessario installare e registrare l'[interfaccia della riga di comando Azure 1.0 più recente](../../xplat-cli-install.md) usando la modalità di Resource Manager nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f2ce6-116">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f2ce6-117">Alcuni esempi di nomi dei parametri sono `myResourceGroup`, `myKeyVault` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="f2ce6-118">Per prima cosa, abilitare il provider dell'insieme di credenziali delle chiavi di Azure nella sottoscrizione di Azure e creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="f2ce6-119">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella posizione `WestUS`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="f2ce6-120">Creare un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="f2ce6-121">Nell'esempio seguente viene creato un insieme di credenziali delle chiavi denominato `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="f2ce6-122">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi e abilitarlo per la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="f2ce6-123">Nell'esempio seguente viene creata una chiave denominata `myKey`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="f2ce6-124">Creare un endpoint tramite Azure Active Directory per gestire l'autenticazione e lo scambio di chiavi di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="f2ce6-125">`--home-page` e `--identifier-uris` non devono necessariamente essere indirizzi instradabili effettivi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="f2ce6-126">Per la massima sicurezza, è preferibile usare i segreti client, anziché le password.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="f2ce6-127">Tuttavia, al momento i segreti client non possono essere generati tramite l'interfaccia della riga di comando di Azure,</span><span class="sxs-lookup"><span data-stu-id="f2ce6-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="f2ce6-128">ma solo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="f2ce6-129">Nell'esempio seguente viene creato un endpoint di Azure Active Directory denominato `myAADApp` con la password `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="f2ce6-130">Specificare una password personalizzata come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="f2ce6-131">Si noti il valore `applicationId` indicato nell'output dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="f2ce6-132">Questo ID applicazione è usato nei passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="f2ce6-133">Aggiungere un disco dati a una VM esistente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="f2ce6-134">Nell'esempio seguente viene aggiunto un disco dati a una VM denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="f2ce6-135">Esaminare i dettagli dell'insieme di credenziali delle chiavi e della chiave creata.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="f2ce6-136">Nel passaggio finale sono necessari l'ID dell'insieme di credenziali delle chiavi, l'URI e l'URL chiave.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="f2ce6-137">Nell'esempio seguente vengono esaminati i dettagli di un insieme di credenziali delle chiavi denominato `myKeyVault` e della chiave denominata `myKey`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="f2ce6-138">Crittografare i dischi come di seguito, immettendo i propri nomi di parametro:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="f2ce6-139">L'interfaccia della riga di comando di Azure non fornisce gli errori dettagliati durante il processo di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="f2ce6-140">Per ulteriori informazioni sulla risoluzione dei problemi, vedere `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="f2ce6-141">Dal momento che il comando precedente dispone di molte variabili e potrebbero non essere fornite molte indicazioni sul perché il processo non riesce, un esempio di comando completo potrebbe essere il seguente:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="f2ce6-142">Riesaminare infine lo stato della crittografia per controllare che ora i dischi virtuali siano crittografati.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="f2ce6-143">Nell'esempio seguente viene controllato lo stato di una VM denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="f2ce6-144">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="f2ce6-144">Overview of disk encryption</span></span>
<span data-ttu-id="f2ce6-145">I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="f2ce6-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="f2ce6-146">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="f2ce6-147">Le chiavi di crittografia vengono archiviate nell'insieme di credenziali delle chiavi di Azure che usano la protezione del software oppure è possibile importare o generare le chiavi in moduli di protezione hardware certificati per gli standard FIPS 140-2 di livello 2.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="f2ce6-148">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="f2ce6-149">Queste chiavi di crittografia vengono usate per crittografare e decrittografare i dischi virtuali collegati alla VM.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="f2ce6-150">Un endpoint di Azure Active Directory fornisce un meccanismo protetto per il rilascio di queste chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="f2ce6-151">Il processo per la crittografia di una VM si articola nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="f2ce6-152">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="f2ce6-153">Configurare la chiave di crittografia in modo da renderla utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="f2ce6-154">Per leggere la chiave di crittografia dall'insieme di credenziali delle chiavi di Azure, creare un endpoint che usa Azure Active Directory con le autorizzazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="f2ce6-155">Eseguire il comando per crittografare i dischi virtuali, specificando l'endpoint di Azure Active Directory e la chiave di crittografia appropriata da usare.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="f2ce6-156">L'endpoint di Azure Active Directory richiede la chiave di crittografia necessaria dall'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="f2ce6-157">I dischi virtuali vengono crittografati tramite la chiave di crittografia fornita.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="f2ce6-158">Servizi di supporto e processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="f2ce6-158">Supporting services and encryption process</span></span>
<span data-ttu-id="f2ce6-159">La crittografia del disco si basa sui componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="f2ce6-160">**Insieme di credenziali delle chiavi di Azure**, che consente di proteggere le chiavi crittografiche e private usate per il processo di crittografia/decrittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="f2ce6-161">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="f2ce6-162">Non è necessario dedicare un insieme di credenziali delle chiavi alla crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="f2ce6-163">Per separare i limiti amministrativi e la visibilità delle chiavi, è possibile creare un insieme di credenziali delle chiavi dedicato.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="f2ce6-164">**Azure Active Directory** gestisce lo scambio protetto delle chiavi di crittografia necessarie e dell'autenticazione per le azioni richieste.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="f2ce6-165">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="f2ce6-166">L'applicazione è sostanzialmente un endpoint tramite cui i servizi delle macchine virtuali e dell'insieme di credenziali delle chiavi possono richiedere e far emettere le chiavi di crittografia appropriate.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="f2ce6-167">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="f2ce6-168">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="f2ce6-168">Requirements and limitations</span></span>
<span data-ttu-id="f2ce6-169">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="f2ce6-170">I seguenti SKU dei server Linux: Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="f2ce6-171">Tutte le risorse, come l'insieme di credenziali delle chiavi, l'account di archiviazione e la VM, devono risiedere nella stessa area e nella stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="f2ce6-172">VM standard delle serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="f2ce6-173">La crittografia del disco non è attualmente supportata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="f2ce6-174">VM di base.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-174">Basic tier VMs.</span></span>
* <span data-ttu-id="f2ce6-175">VM create con il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="f2ce6-176">Disabilitare la crittografia del disco del sistema operativo nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="f2ce6-177">Aggiornare le chiavi di crittografia in una VM Linux già crittografata.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="f2ce6-178">Creare le chiavi e l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="f2ce6-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="f2ce6-179">Per completare il resto della presente guida, è necessario installare e registrare l'[ultima versione dell'interfaccia della riga di comando di Azure 1.0](../../xplat-cli-install.md) usando la modalità di Resource Manager nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f2ce6-180">Negli esempi di comandi sostituire tutti i parametri di esempio con i propri valori di nome, percorso e chiave.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="f2ce6-181">Negli esempi viene usata una convenzione di `myResourceGroup`, `myKeyVault`, `myAADApp` e così via.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="f2ce6-182">Il primo passaggio consiste nel creare un insieme di credenziali delle chiavi di Azure in cui archiviare le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="f2ce6-183">L'insieme di credenziali delle chiavi di Azure consente di archiviare chiavi, chiavi private o password da implementare in tutta sicurezza in applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="f2ce6-184">Per la crittografia del disco virtuale, usare l'insieme di credenziali delle chiavi per archiviare una chiave di crittografia usata per crittografare o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="f2ce6-185">Abilitare il provider dell'insieme di credenziali delle chiavi di Azure nella sottoscrizione di Azure, quindi creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="f2ce6-186">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `WestUS`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="f2ce6-187">L'insieme di credenziali delle chiavi di Azure contenente le chiavi di crittografia e le risorse di calcolo associate, come l'archiviazione e la VM stessa, devono risiedere nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="f2ce6-188">Nell'esempio seguente viene creato un insieme di credenziali delle chiavi di Azure denominato `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="f2ce6-189">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="f2ce6-190">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="f2ce6-191">Esiste un costo aggiuntivo per creare un insieme di credenziali delle chiavi premium, anziché standard, in cui archiviare le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="f2ce6-192">Per creare un insieme di credenziali delle chiavi premium, aggiungere `--sku Premium` al comando del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="f2ce6-193">L'esempio seguente usa chiavi protette tramite software, poiché viene creato un insieme di credenziali delle chiavi standard.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="f2ce6-194">Per entrambi i modelli di protezione, è necessario consentire alla piattaforma Azure di accedere all'avvio della VM per richiedere le chiavi di crittografia con cui decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="f2ce6-195">Creare una chiave di crittografia all'interno dell'insieme di credenziali delle chiavi, quindi abilitarne l'uso con la crittografia del disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="f2ce6-196">Nell'esempio seguente viene creata una chiave denominata `myKey`, successivamente abilitata per la crittografia del disco:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="f2ce6-197">Creare l'applicazione di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2ce6-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="f2ce6-198">Al momento di crittografare o decrittografare i dischi virtuali, un endpoint gestisce l'autenticazione e lo scambio delle chiavi di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="f2ce6-199">Questo endpoint, un'applicazione di Azure Active Directory, consente alla piattaforma Azure di richiedere le chiavi di crittografia appropriate per conto della VM.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="f2ce6-200">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="f2ce6-201">Poiché non si intende creare un'applicazione di Azure Active Directory completa, nell'esempio seguente i parametri `--home-page` e `--identifier-uris` non devono necessariamente essere indirizzi instradabili effettivi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="f2ce6-202">Nell'esempio seguente viene inoltre specificata una chiave privata basata su password, anziché generare chiavi dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="f2ce6-203">Attualmente non è possibile generare chiavi dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="f2ce6-204">Creare l'applicazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="f2ce6-205">Nell'esempio seguente viene creata un'applicazione denominata `myAADApp` che usa la password `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="f2ce6-206">Specificare una password personalizzata come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="f2ce6-207">Prendere nota del valore `applicationId` restituito nell'output del comando precedente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="f2ce6-208">L'ID applicazione verrà usato in alcuni dei passaggi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="f2ce6-209">Creare quindi un nome dell'entità servizio per rendere accessibile l'applicazione all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="f2ce6-210">Per crittografare o decrittografare correttamente i dischi virtuali, le autorizzazioni per la chiave di crittografia archiviata nell'insieme di credenziali delle chiavi devono essere impostate in modo tale da consentire all'applicazione di Azure Active Directory di leggere le chiavi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="f2ce6-211">Creare il nome dell'entità servizio e impostare le autorizzazioni appropriate, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="f2ce6-212">Aggiungere un disco virtuale ed esaminare lo stato di crittografia</span><span class="sxs-lookup"><span data-stu-id="f2ce6-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="f2ce6-213">Per crittografare alcuni dischi virtuali, è possibile aggiungere un disco a una VM esistente.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="f2ce6-214">Aggiungere un disco dati da 5 GB a una VM esistente come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="f2ce6-215">I dischi virtuali non sono attualmente crittografati.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="f2ce6-216">Controllare l'attuale stato di crittografia della VM come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="f2ce6-217">Crittografare i dischi virtuali</span><span class="sxs-lookup"><span data-stu-id="f2ce6-217">Encrypt virtual disks</span></span>
<span data-ttu-id="f2ce6-218">A questo punto, per crittografare i dischi virtuali, vengono riuniti tutti i componenti precedenti:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="f2ce6-219">Specificare l'applicazione di Azure Active Directory e la relativa password.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="f2ce6-220">Specificare l'insieme di credenziali delle chiavi in cui memorizzare i metadati dei dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="f2ce6-221">Specificare le chiavi di crittografia da usare per la crittografia e la decrittografia effettive.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="f2ce6-222">Specificare se si desidera crittografare il disco del sistema operativo, i dischi dati o tutti i dischi.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="f2ce6-223">Controllare i dettagli dell'insieme di credenziali delle chiavi di Azure e la chiave creata, in quanto nel passaggio finale sono necessari l'ID dell'insieme di credenziali delle chiavi, l'URI e l'URL della chiave:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="f2ce6-224">Crittografare il disco virtuale usando l'output dei comandi `azure keyvault show` e `azure keyvault key show` nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="f2ce6-225">Poiché il comando precedente ha molte variabili, l'esempio seguente contiene il comando completo come riferimento:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="f2ce6-226">L'interfaccia della riga di comando di Azure non fornisce gli errori dettagliati durante il processo di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="f2ce6-227">Per ulteriori informazioni sulla risoluzione dei problemi, vedere `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` sulla VM da crittografare.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="f2ce6-228">Riesaminare infine lo stato della crittografia per controllare che ora i dischi virtuali siano crittografati:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="f2ce6-229">Aggiungere ulteriori dischi dati</span><span class="sxs-lookup"><span data-stu-id="f2ce6-229">Add additional data disks</span></span>
<span data-ttu-id="f2ce6-230">Una volta crittografati i dischi dati, in un secondo momento è possibile aggiungere alla VM ulteriori dischi virtuali e anche crittografarli.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="f2ce6-231">Quando si esegue il comando `azure vm enable-disk-encryption`, incrementare la versione di sequenza usando il parametro `--sequence-version`.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="f2ce6-232">Questo parametro della versione di sequenza consente di eseguire ripetutamente operazioni sulla stessa VM.</span><span class="sxs-lookup"><span data-stu-id="f2ce6-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="f2ce6-233">Ad esempio, consente di aggiungere alla VM un secondo disco virtuale, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="f2ce6-234">Eseguire nuovamente il comando per crittografare i dischi virtuali, questa volta aggiungendo il parametro `--sequence-version` e incrementando il valore della prima esecuzione, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="f2ce6-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="f2ce6-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2ce6-235">Next steps</span></span>
* <span data-ttu-id="f2ce6-236">Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="f2ce6-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="f2ce6-237">Per altre informazioni sulla crittografia del disco, tra cui come preparare una VM personalizzata con crittografia da caricare in Azure, vedere [Crittografia dischi di Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="f2ce6-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
