---
title: aaaEncrypt dischi in una VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Come tooencrypt dischi in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="5d4e1-103">Crittografare i dischi in una VM Linux utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5d4e1-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="5d4e1-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati a riposo.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="5d4e1-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="5d4e1-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="5d4e1-107">In questo articolo illustra in dettaglio come tooencrypt dischi virtuali in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="5d4e1-108">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="5d4e1-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="5d4e1-109">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="5d4e1-110">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="5d4e1-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5d4e1-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="5d4e1-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5d4e1-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="5d4e1-112">Quick commands</span></span>
<span data-ttu-id="5d4e1-113">Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base comandi tooencrypt dischi virtuali nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="5d4e1-114">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="5d4e1-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="5d4e1-115">È necessario hello [più recente di Azure CLI 1.0](../../xplat-cli-install.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5d4e1-116">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5d4e1-117">I nomi dei parametri di esempio includono `myResourceGroup`, `myKeyVault` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="5d4e1-118">Innanzitutto, abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure e creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="5d4e1-119">esempio Hello crea il nome di un gruppo di risorse `myResourceGroup` in hello `WestUS` percorso:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="5d4e1-120">Creare un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="5d4e1-121">esempio Hello crea un insieme di credenziali di chiave denominato `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="5d4e1-122">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi e abilitarlo per la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="5d4e1-123">esempio Hello crea una chiave denominata `myKey`:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="5d4e1-124">Creare un endpoint tramite Azure Active Directory per la gestione dell'autenticazione hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="5d4e1-125">Hello `--home-page` e `--identifier-uris` non è necessario l'indirizzo instradabile effettivo toobe.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="5d4e1-126">Per hello massimo livello di sicurezza, i segreti del client devono essere utilizzati anziché le password.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="5d4e1-127">Hello CLI di Azure attualmente non è possibile generare i segreti dei client.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="5d4e1-128">I segreti dei client possono essere generati solo nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="5d4e1-129">esempio Hello crea un endpoint di Azure Active Directory denominato `myAADApp` e viene utilizzata una password di `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="5d4e1-130">Specificare una password personalizzata come di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="5d4e1-131">Hello nota `applicationId` illustrato nell'output di hello da hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="5d4e1-132">Questo ID applicazione viene utilizzato in hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="5d4e1-133">Aggiungere un tooan disco dati macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="5d4e1-134">esempio Hello aggiunge un tooa disco dati macchina virtuale denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5d4e1-135">Esaminare i dettagli di hello per la chiave di insieme di credenziali chiave e hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="5d4e1-136">È necessario hello ID insieme di credenziali chiave, URI e chiave URL nel passaggio finale hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="5d4e1-137">Hello esempio esamina i dettagli di hello per un insieme di credenziali di chiave denominato `myKeyVault` e una chiave denominata `myKey`:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="5d4e1-138">Crittografare i dischi come di seguito, immettendo i propri nomi di parametro:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="5d4e1-139">Hello CLI di Azure non fornisce gli errori dettagliati durante il processo di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="5d4e1-140">Per ulteriori informazioni sulla risoluzione dei problemi, vedere `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="5d4e1-141">Come hello precedente comando dispone di molte variabili e potrebbero non essere molto indicazione as avrà esito negativo processo di hello toowhy, un esempio di comandi completo potrebbe essere come segue:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="5d4e1-142">Infine, esaminare lo stato di crittografia hello nuovamente tooconfirm che i dischi virtuali sono ora stati crittografati.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="5d4e1-143">esempio Hello Controlla stato hello di una macchina virtuale denominata `myVM` in hello `myResourceGroup` gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="5d4e1-144">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="5d4e1-144">Overview of disk encryption</span></span>
<span data-ttu-id="5d4e1-145">I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="5d4e1-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="5d4e1-146">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="5d4e1-147">Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="5d4e1-148">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="5d4e1-149">Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="5d4e1-150">Un endpoint di Azure Active Directory fornisce un meccanismo protetto per il rilascio di queste chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="5d4e1-151">il processo di Hello per la crittografia di una macchina virtuale è il seguente:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="5d4e1-152">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="5d4e1-153">Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="5d4e1-154">chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un endpoint tramite Azure Active Directory con le autorizzazioni appropriate di hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="5d4e1-155">Eseguire hello comando tooencrypt i dischi virtuali, specificando l'endpoint di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="5d4e1-156">endpoint di Azure Active Directory Hello richiede la chiave di crittografia richiesto di hello insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="5d4e1-157">i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="5d4e1-158">Servizi di supporto e processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="5d4e1-158">Supporting services and encryption process</span></span>
<span data-ttu-id="5d4e1-159">Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="5d4e1-160">**Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="5d4e1-161">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="5d4e1-162">Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="5d4e1-163">limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="5d4e1-164">**Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="5d4e1-165">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="5d4e1-166">un'applicazione Hello è più un endpoint per l'insieme di credenziali chiave hello e toorequest servizi macchina virtuale e ottenere generato le chiavi di crittografia appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="5d4e1-167">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="5d4e1-168">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="5d4e1-168">Requirements and limitations</span></span>
<span data-ttu-id="5d4e1-169">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="5d4e1-170">Hello seguente server Linux SKU - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="5d4e1-171">Tutte le risorse (ad esempio l'insieme di credenziali chiave, l'account di archiviazione e macchina virtuale) devono essere in hello stessa regione di Azure e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="5d4e1-172">VM standard delle serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="5d4e1-173">Crittografia del disco non è attualmente supportata nei seguenti scenari hello:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="5d4e1-174">VM di base.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-174">Basic tier VMs.</span></span>
* <span data-ttu-id="5d4e1-175">Macchine virtuali create con modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="5d4e1-176">Disabilitare la crittografia del disco del sistema operativo nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="5d4e1-177">Aggiornamento delle chiavi di crittografia in una VM Linux già crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="5d4e1-178">Creare hello insieme credenziali chiavi Azure e le chiavi</span><span class="sxs-lookup"><span data-stu-id="5d4e1-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="5d4e1-179">toocomplete hello restanti in questa Guida, è necessario hello [più recente di Azure CLI 1.0](../../xplat-cli-install.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5d4e1-180">Nel corso di esempi di comandi hello, sostituire tutti i parametri di esempio con i nomi, percorso e i valori di chiave.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="5d4e1-181">Negli esempi seguenti Hello utilizzano una convenzione di `myResourceGroup`, `myKeyVault`, `myAADApp`e così via.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="5d4e1-182">primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="5d4e1-183">Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="5d4e1-184">Per la crittografia del disco virtuale, si usa l'insieme di credenziali chiave toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="5d4e1-185">Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure, quindi creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="5d4e1-186">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUS` percorso:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="5d4e1-187">Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="5d4e1-188">esempio Hello crea un insieme di credenziali chiave di Azure denominato `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="5d4e1-189">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="5d4e1-190">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="5d4e1-191">È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="5d4e1-192">aggiungere un insieme di credenziali chiave premium nel precedente passaggio hello toocreate `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="5d4e1-193">Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="5d4e1-194">Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="5d4e1-195">Creare una chiave di crittografia all'interno dell'insieme di credenziali delle chiavi, quindi abilitarne l'uso con la crittografia del disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="5d4e1-196">esempio Hello crea una chiave denominata `myKey` e quindi lo abilita per la crittografia del disco:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="5d4e1-197">Creare un'applicazione hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d4e1-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="5d4e1-198">Quando i dischi virtuali vengono crittografati o decrittografati, si utilizza un'autenticazione hello toohandle di endpoint e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="5d4e1-199">Questo endpoint, un'applicazione Azure Active Directory, consente di hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="5d4e1-200">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="5d4e1-201">Come si sta creando un'applicazione Azure Active Directory completa, hello `--home-page` e `--identifier-uris` parametri nel seguente esempio hello non richiedono l'indirizzo instradabile effettivo toobe.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="5d4e1-202">Hello esempio specifica inoltre un segreto basato su password, anziché la generazione di chiavi all'interno di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="5d4e1-203">In questo momento, è Impossibile eseguire la generazione di chiavi da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="5d4e1-204">Creare l'applicazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="5d4e1-205">esempio Hello crea un'applicazione denominata `myAADApp` e viene utilizzata una password di `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="5d4e1-206">Specificare una password personalizzata come di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="5d4e1-207">Prendere nota di hello `applicationId` restituito nell'output di hello da hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="5d4e1-208">Questo ID applicazione viene utilizzato in alcune hello rimanenti passaggi.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="5d4e1-209">Creare quindi un nome dell'entità servizio (SPN) in modo che un'applicazione hello è accessibile all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="5d4e1-210">toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere tooread hello chiavi del set toopermit hello Azure Active Directory dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="5d4e1-211">Creare hello SPN e impostare le autorizzazioni appropriate di hello come segue:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="5d4e1-212">Aggiungere un disco virtuale ed esaminare lo stato di crittografia</span><span class="sxs-lookup"><span data-stu-id="5d4e1-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="5d4e1-213">tooactually crittografare alcuni dischi virtuali, consente di aggiungere un disco tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="5d4e1-214">Aggiungere un tooan disco dati di 5Gb esistente VM come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5d4e1-215">i dischi virtuali Hello attualmente non sono crittografati.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="5d4e1-216">Controllare hello stato corrente di crittografia di una macchina virtuale come segue:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="5d4e1-217">Crittografare i dischi virtuali</span><span class="sxs-lookup"><span data-stu-id="5d4e1-217">Encrypt virtual disks</span></span>
<span data-ttu-id="5d4e1-218">toonow crittografare i dischi virtuali hello, riunire tutti i componenti precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="5d4e1-219">Specificare un'applicazione hello Azure Active Directory e la password.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="5d4e1-220">Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="5d4e1-221">Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="5d4e1-222">Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="5d4e1-223">Consente di esaminare i dettagli di hello per la chiave di insieme di credenziali chiave di Azure e hello che è stato creato, come necessario hello ID insieme di credenziali chiave, URI e quindi digitare un URL passaggio finale hello:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="5d4e1-224">Crittografare i dischi virtuali tramite output di hello dalla hello `azure keyvault show` e `azure keyvault key show` comandi nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="5d4e1-225">Come hello precedente comando dispone di numerose variabili, hello esempio seguente è di comandi completo per il riferimento hello:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

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

<span data-ttu-id="5d4e1-226">Hello CLI di Azure non fornisce gli errori dettagliati durante il processo di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="5d4e1-227">Per ulteriori informazioni sulla risoluzione dei problemi, esaminare `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` su hello VM si esegue la crittografia.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="5d4e1-228">Infine, consente di esaminare lo stato di crittografia hello nuovamente tooconfirm che i dischi virtuali ora sono stati crittografati:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="5d4e1-229">Aggiungere ulteriori dischi dati</span><span class="sxs-lookup"><span data-stu-id="5d4e1-229">Add additional data disks</span></span>
<span data-ttu-id="5d4e1-230">Dopo che sono stati crittografati i dischi dati, è possibile in seguito si aggiungono altri dischi virtuali tooyour VM e anche crittografarle.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="5d4e1-231">Quando si esegue hello `azure vm enable-disk-encryption` comando, incremento hello sequenza versione che utilizza hello `--sequence-version` parametro.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="5d4e1-232">Questo parametro di versione sequenza consente tooperform ripetute operazioni con hello stessa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d4e1-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="5d4e1-233">Ad esempio, consente di aggiungere un secondo tooyour disco virtuale VM come segue:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5d4e1-234">Eseguire di nuovo hello comando tooencrypt hello dischi virtuali, questa volta aggiungendo hello `--sequence-version` parametro e incremento hello compreso il primo eseguire come segue:</span><span class="sxs-lookup"><span data-stu-id="5d4e1-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="5d4e1-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d4e1-235">Next steps</span></span>
* <span data-ttu-id="5d4e1-236">Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="5d4e1-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="5d4e1-237">Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="5d4e1-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
