---
title: aaaEncrypt dischi in una VM Linux di Azure | Documenti Microsoft
description: Come tooencrypt dischi virtuali in una VM Linux per l'utilizzo di protezione avanzata hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="f6e50-103">Come tooencrypt dischi virtuali in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="f6e50-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="f6e50-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati.</span><span class="sxs-lookup"><span data-stu-id="f6e50-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="f6e50-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e50-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="f6e50-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="f6e50-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="f6e50-107">In questo articolo illustra in dettaglio come tooencrypt dischi virtuali in una VM Linux utilizzando hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f6e50-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="f6e50-108">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6e50-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f6e50-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="f6e50-109">Quick commands</span></span>
<span data-ttu-id="f6e50-110">Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base comandi tooencrypt dischi virtuali nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6e50-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="f6e50-111">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="f6e50-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="f6e50-112">È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f6e50-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f6e50-113">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f6e50-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f6e50-114">I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f6e50-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="f6e50-115">Innanzitutto, abilitare il provider insieme credenziali chiavi Azure hello nella sottoscrizione di Azure con [registro provider az](/cli/azure/provider#register) e creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f6e50-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f6e50-116">esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="f6e50-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f6e50-117">Creare un insieme di credenziali chiave di Azure con [keyvault az creare](/cli/azure/keyvault#create) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="f6e50-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="f6e50-118">Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f6e50-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="f6e50-119">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="f6e50-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="f6e50-120">esempio Hello crea una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="f6e50-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="f6e50-121">Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="f6e50-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="f6e50-122">handle dell'entità servizio di Hello hello autenticazione e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f6e50-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="f6e50-123">Hello di esempio seguente legge i valori hello per un'entità servizio hello Id e la password per l'uso nei comandi di versioni successive:</span><span class="sxs-lookup"><span data-stu-id="f6e50-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="f6e50-124">password Hello viene restituita solo quando si crea hello dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="f6e50-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="f6e50-125">Se si desidera, visualizzare e registrare hello password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="f6e50-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="f6e50-126">È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="f6e50-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="f6e50-127">Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="f6e50-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="f6e50-128">Nell'esempio seguente di hello, hello ID entità servizio viene fornito da hello precedente comando:</span><span class="sxs-lookup"><span data-stu-id="f6e50-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="f6e50-129">Creare una macchina virtuale con [az vm create](/cli/azure/vm#create) e collegare un disco dati di 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="f6e50-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="f6e50-130">Solo determinate immagini di marketplace supportano la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="f6e50-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="f6e50-131">esempio Hello crea una macchina virtuale denominata `myVM` utilizzando un **CentOS 7.2n** immagine:</span><span class="sxs-lookup"><span data-stu-id="f6e50-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="f6e50-132">SSH tramite VM tooyour hello `publicIpAddress` illustrato nell'output di hello di hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="f6e50-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="f6e50-133">Creare una partizione e un file System, quindi montare il disco di dati hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="f6e50-134">Per ulteriori informazioni, vedere [connettersi tooa nuovo disco VM Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="f6e50-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="f6e50-135">Chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="f6e50-135">Close your SSH session.</span></span>

<span data-ttu-id="f6e50-136">Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="f6e50-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="f6e50-137">esempio Hello utilizza hello `$sp_id` e `$sp_password` variabili da hello precedente `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="f6e50-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="f6e50-138">Comporta un tempo per hello disco crittografia processo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f6e50-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="f6e50-139">Monitorare lo stato di hello del processo di hello con [Mostra la crittografia di vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="f6e50-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-140">Mostra lo stato di Hello **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="f6e50-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="f6e50-141">Attendere fino a quando lo stato di hello report del disco del sistema operativo hello **VMRestartPending**, quindi riavviare la macchina virtuale con [riavvio vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="f6e50-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-142">Hello il processo di crittografia del disco è finalizzato durante il processo di avvio di hello, quindi attendere qualche minuto prima di archiviare lo stato di hello di crittografia con **Mostra la crittografia di vm az**:</span><span class="sxs-lookup"><span data-stu-id="f6e50-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-143">stato Hello deve segnalare ora sia disco hello del sistema operativo e dati come **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="f6e50-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="f6e50-144">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="f6e50-144">Overview of disk encryption</span></span>
<span data-ttu-id="f6e50-145">I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="f6e50-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="f6e50-146">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e50-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="f6e50-147">Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2.</span><span class="sxs-lookup"><span data-stu-id="f6e50-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="f6e50-148">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="f6e50-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="f6e50-149">Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6e50-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="f6e50-150">Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="f6e50-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="f6e50-151">il processo di Hello per la crittografia di una macchina virtuale è il seguente:</span><span class="sxs-lookup"><span data-stu-id="f6e50-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="f6e50-152">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e50-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="f6e50-153">Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="f6e50-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="f6e50-154">chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un servizio di Azure Active Directory principale con le autorizzazioni appropriate di hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="f6e50-155">Eseguire hello comando tooencrypt i dischi virtuali, specifica dell'entità servizio di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.</span><span class="sxs-lookup"><span data-stu-id="f6e50-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="f6e50-156">le entità richieste di servizio Azure Active Directory Hello hello chiave di crittografia richiesto dall'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e50-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="f6e50-157">i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.</span><span class="sxs-lookup"><span data-stu-id="f6e50-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="f6e50-158">Processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="f6e50-158">Encryption process</span></span>
<span data-ttu-id="f6e50-159">Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f6e50-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="f6e50-160">**Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco.</span><span class="sxs-lookup"><span data-stu-id="f6e50-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="f6e50-161">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="f6e50-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="f6e50-162">Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f6e50-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="f6e50-163">limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.</span><span class="sxs-lookup"><span data-stu-id="f6e50-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="f6e50-164">**Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni.</span><span class="sxs-lookup"><span data-stu-id="f6e50-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="f6e50-165">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6e50-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="f6e50-166">entità servizio Hello fornisce un meccanismo protetto di toorequest e generato le chiavi di crittografia appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="f6e50-167">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6e50-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="f6e50-168">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="f6e50-168">Requirements and limitations</span></span>
<span data-ttu-id="f6e50-169">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="f6e50-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="f6e50-170">Hello seguente server Linux SKU - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="f6e50-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="f6e50-171">Tutte le risorse (ad esempio l'insieme di credenziali chiave, l'account di archiviazione e macchina virtuale) devono essere in hello stessa regione di Azure e sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f6e50-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="f6e50-172">VM standard delle serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="f6e50-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="f6e50-173">Crittografia del disco non è attualmente supportata nei seguenti scenari hello:</span><span class="sxs-lookup"><span data-stu-id="f6e50-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="f6e50-174">VM di base.</span><span class="sxs-lookup"><span data-stu-id="f6e50-174">Basic tier VMs.</span></span>
* <span data-ttu-id="f6e50-175">Macchine virtuali create con modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="f6e50-176">Disabilitare la crittografia del disco del sistema operativo nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="f6e50-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="f6e50-177">Aggiornamento delle chiavi di crittografia in una VM Linux già crittografato hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="f6e50-178">Creare le chiavi e l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="f6e50-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="f6e50-179">È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f6e50-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="f6e50-180">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f6e50-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f6e50-181">I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f6e50-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="f6e50-182">primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="f6e50-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="f6e50-183">Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="f6e50-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="f6e50-184">Per la crittografia del disco virtuale, si usa l'insieme di credenziali chiave toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="f6e50-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="f6e50-185">Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure con [registro provider az](/cli/azure/provider#register) e creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f6e50-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f6e50-186">esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello `eastus` percorso:</span><span class="sxs-lookup"><span data-stu-id="f6e50-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="f6e50-187">Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="f6e50-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="f6e50-188">Creare un insieme di credenziali chiave di Azure con [keyvault az creare](/cli/azure/keyvault#create) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="f6e50-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="f6e50-189">Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f6e50-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="f6e50-190">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="f6e50-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="f6e50-191">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="f6e50-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="f6e50-192">È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="f6e50-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="f6e50-193">aggiungere un insieme di credenziali chiave premium nel precedente passaggio hello toocreate `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="f6e50-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="f6e50-194">Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard.</span><span class="sxs-lookup"><span data-stu-id="f6e50-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="f6e50-195">Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6e50-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="f6e50-196">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="f6e50-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="f6e50-197">esempio Hello crea una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="f6e50-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="f6e50-198">Creare hello dell'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6e50-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="f6e50-199">Quando i dischi virtuali vengono crittografati o decrittografati, specificare l'autenticazione di account toohandle hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="f6e50-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="f6e50-200">Questo account, un'entità di servizio di Azure Active Directory consente hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6e50-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="f6e50-201">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="f6e50-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="f6e50-202">Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="f6e50-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="f6e50-203">Hello di esempio seguente legge i valori hello per un'entità servizio hello Id e la password per l'uso nei comandi di versioni successive:</span><span class="sxs-lookup"><span data-stu-id="f6e50-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="f6e50-204">password di Hello viene visualizzata solo quando si crea il servizio di hello principale.</span><span class="sxs-lookup"><span data-stu-id="f6e50-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="f6e50-205">Se si desidera, visualizzare e registrare hello password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="f6e50-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="f6e50-206">È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="f6e50-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="f6e50-207">toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere principale tooread hello chiavi del set toopermit hello Azure Active Directory del servizio.</span><span class="sxs-lookup"><span data-stu-id="f6e50-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="f6e50-208">Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="f6e50-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="f6e50-209">Nell'esempio seguente di hello, hello ID entità servizio viene fornito da hello precedente comando:</span><span class="sxs-lookup"><span data-stu-id="f6e50-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="f6e50-210">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f6e50-210">Create virtual machine</span></span>
<span data-ttu-id="f6e50-211">tooactually crittografare alcuni dischi virtuali, consente di creare una macchina virtuale e aggiungere un disco dati.</span><span class="sxs-lookup"><span data-stu-id="f6e50-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="f6e50-212">Creare una macchina virtuale tooencrypt con [creare vm az](/cli/azure/vm#create) e collegare un disco dati di 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="f6e50-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="f6e50-213">Solo determinate immagini di marketplace supportano la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="f6e50-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="f6e50-214">esempio Hello crea una macchina virtuale denominata *myVM* utilizzando un **CentOS 7.2n** immagine:</span><span class="sxs-lookup"><span data-stu-id="f6e50-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="f6e50-215">SSH tramite VM tooyour hello `publicIpAddress` illustrato nell'output di hello di hello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="f6e50-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="f6e50-216">Creare una partizione e un file System, quindi montare il disco di dati hello.</span><span class="sxs-lookup"><span data-stu-id="f6e50-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="f6e50-217">Per ulteriori informazioni, vedere [connettersi tooa nuovo disco VM Linux toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="f6e50-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="f6e50-218">Chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="f6e50-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="f6e50-219">Crittografare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f6e50-219">Encrypt virtual machine</span></span>
<span data-ttu-id="f6e50-220">tooencrypt hello i dischi virtuali, riunire tutti i componenti precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="f6e50-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="f6e50-221">Specificare hello entità servizio di Azure Active Directory e una password.</span><span class="sxs-lookup"><span data-stu-id="f6e50-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="f6e50-222">Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="f6e50-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="f6e50-223">Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.</span><span class="sxs-lookup"><span data-stu-id="f6e50-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="f6e50-224">Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.</span><span class="sxs-lookup"><span data-stu-id="f6e50-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="f6e50-225">Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="f6e50-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="f6e50-226">esempio Hello utilizza hello `$sp_id` e `$sp_password` variabili da hello precedente `ad sp create-for-rbac` comando:</span><span class="sxs-lookup"><span data-stu-id="f6e50-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="f6e50-227">Comporta un tempo per hello disco crittografia processo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f6e50-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="f6e50-228">Monitorare lo stato di hello del processo di hello con [Mostra la crittografia di vm az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="f6e50-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-229">l'output è simile toohello seguente esempio troncato Hello:</span><span class="sxs-lookup"><span data-stu-id="f6e50-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="f6e50-230">Attendere fino a quando lo stato di hello report del disco del sistema operativo hello **VMRestartPending**, quindi riavviare la macchina virtuale con [riavvio vm az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="f6e50-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-231">Hello il processo di crittografia del disco è finalizzato durante il processo di avvio di hello, quindi attendere qualche minuto prima di archiviare lo stato di hello di crittografia con **Mostra la crittografia di vm az**:</span><span class="sxs-lookup"><span data-stu-id="f6e50-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f6e50-232">stato Hello deve segnalare ora sia disco hello del sistema operativo e dati come **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="f6e50-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="f6e50-233">Aggiungere ulteriori dischi dati</span><span class="sxs-lookup"><span data-stu-id="f6e50-233">Add additional data disks</span></span>
<span data-ttu-id="f6e50-234">Dopo che sono stati crittografati i dischi dati, è possibile in seguito si aggiungono altri dischi virtuali tooyour VM e anche crittografarle.</span><span class="sxs-lookup"><span data-stu-id="f6e50-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="f6e50-235">Ad esempio, consente di aggiungere un secondo tooyour disco virtuale VM come segue:</span><span class="sxs-lookup"><span data-stu-id="f6e50-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="f6e50-236">Eseguire di nuovo hello comando tooencrypt hello i dischi virtuali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="f6e50-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="f6e50-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f6e50-237">Next steps</span></span>
* <span data-ttu-id="f6e50-238">Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="f6e50-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="f6e50-239">Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="f6e50-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
