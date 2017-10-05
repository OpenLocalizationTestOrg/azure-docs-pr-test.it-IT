---
title: Crittografare i dischi di una macchina virtuale Linux | Documentazione Microsoft
description: Come crittografare i dischi virtuali in una VM di Linux per una maggiore sicurezza tramite l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="e2537-103">Come crittografare i dischi virtuali in una VM di Linux</span><span class="sxs-lookup"><span data-stu-id="e2537-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="e2537-104">Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati.</span><span class="sxs-lookup"><span data-stu-id="e2537-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="e2537-105">I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2537-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="e2537-106">È possibile controllare queste chiavi di crittografia e il loro uso.</span><span class="sxs-lookup"><span data-stu-id="e2537-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e2537-107">Questo articolo descrive come crittografare i dischi virtuali in una VM di Linux tramite l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="e2537-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="e2537-108">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2537-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e2537-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="e2537-109">Quick commands</span></span>
<span data-ttu-id="e2537-110">Se si necessita di eseguire rapidamente l'attività, nella sezione seguente sono illustrati i comandi di base per crittografare i dischi rigidi della VM.</span><span class="sxs-lookup"><span data-stu-id="e2537-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="e2537-111">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="e2537-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="e2537-112">È necessario aver installato l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e2537-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="e2537-113">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="e2537-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e2537-114">I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="e2537-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="e2537-115">Per prima cosa, abilitare il provider dell'insieme di credenziali delle chiavi di Azure nella sottoscrizione di Azure con [az provider register](/cli/azure/provider#register) e creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2537-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e2537-116">L'esempio seguente crea un nome del gruppo di risorse *myResourceGroup* nella località *stati uniti orientali*:</span><span class="sxs-lookup"><span data-stu-id="e2537-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e2537-117">Creare un insieme di credenziali delle chiavi di Azure con [az keyvault create](/cli/azure/keyvault#create) e abilitare l'insieme di credenziali delle chiavi per l'utilizzo con crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="e2537-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="e2537-118">Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2537-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="e2537-119">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="e2537-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="e2537-120">Nell'esempio seguente viene creata una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="e2537-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="e2537-121">Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="e2537-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="e2537-122">L'entità servizio gestisce l'autenticazione e lo scambio di chiavi di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="e2537-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e2537-123">Nell'esempio seguente vengono letti i valori per l'ID e la password dell'entità servizio per l'uso nei comandi successivi:</span><span class="sxs-lookup"><span data-stu-id="e2537-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="e2537-124">La password viene restituita solo quando si crea l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="e2537-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="e2537-125">Se lo si desidera, visualizzare e registrare la password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="e2537-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="e2537-126">È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="e2537-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="e2537-127">Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="e2537-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="e2537-128">Nell'esempio seguente l'ID dell'entità servizio viene fornita dal comando precedente:</span><span class="sxs-lookup"><span data-stu-id="e2537-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="e2537-129">Creare una macchina virtuale con [az vm create](/cli/azure/vm#create) e collegare un disco dati di 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="e2537-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="e2537-130">Solo determinate immagini di marketplace supportano la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="e2537-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="e2537-131">Nell'esempio seguente viene creata una VM denominata `myVM` usando un'immagine **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="e2537-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="e2537-132">SSH per la macchina virtuale tramite il valore `publicIpAddress` indicato nell'output dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="e2537-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="e2537-133">Creare una partizione e un file system, quindi montare il disco dati.</span><span class="sxs-lookup"><span data-stu-id="e2537-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="e2537-134">Per ulteriori informazioni, vedere [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk) (Connettersi a una VM Linux per montare il nuovo disco).</span><span class="sxs-lookup"><span data-stu-id="e2537-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="e2537-135">Chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="e2537-135">Close your SSH session.</span></span>

<span data-ttu-id="e2537-136">Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="e2537-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="e2537-137">Nell'esempio seguente vengono usate le variabili `$sp_id` e `$sp_password` dal comando precedente `ad sp create-for-rbac`:</span><span class="sxs-lookup"><span data-stu-id="e2537-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="e2537-138">Il completamento del processo di crittografia del disco richiede qualche istante.</span><span class="sxs-lookup"><span data-stu-id="e2537-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="e2537-139">Monitorare lo stato del processo con [z vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="e2537-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-140">Lo stato mostra **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="e2537-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="e2537-141">Attendere che lo stato per il sistema operativo del disco indichi **VMRestartPending**, quindi riavviare la macchina virtuale con [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="e2537-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-142">Il processo di crittografia del disco è finalizzato durante il processo di avvio, pertanto, attendere alcuni minuti prima di verificare di nuovo lo stato della crittografia con **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="e2537-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-143">Lo stato dovrebbe ora segnalare sia il disco del sistema operativo che il disco dati come **Crittografato**.</span><span class="sxs-lookup"><span data-stu-id="e2537-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="e2537-144">Panoramica della crittografia dei dischi</span><span class="sxs-lookup"><span data-stu-id="e2537-144">Overview of disk encryption</span></span>
<span data-ttu-id="e2537-145">I dischi virtuali delle VM Linux vengono crittografati a riposo mediante [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="e2537-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="e2537-146">Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2537-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="e2537-147">Le chiavi di crittografia vengono archiviate nell'insieme di credenziali delle chiavi di Azure che usano la protezione del software oppure è possibile importare o generare le chiavi in moduli di protezione hardware certificati per gli standard FIPS 140-2 di livello 2.</span><span class="sxs-lookup"><span data-stu-id="e2537-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="e2537-148">È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso.</span><span class="sxs-lookup"><span data-stu-id="e2537-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e2537-149">Queste chiavi di crittografia vengono usate per crittografare e decrittografare i dischi virtuali collegati alla VM.</span><span class="sxs-lookup"><span data-stu-id="e2537-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="e2537-150">Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.</span><span class="sxs-lookup"><span data-stu-id="e2537-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="e2537-151">Il processo per la crittografia di una VM si articola nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="e2537-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="e2537-152">Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2537-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="e2537-153">Configurare la chiave di crittografia in modo da renderla utilizzabile per la crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="e2537-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="e2537-154">Per leggere la chiave di crittografia dall'insieme di credenziali delle chiavi di Azure, creare un'entità servizio di Azure Active Directory con le autorizzazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="e2537-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="e2537-155">Eseguire il comando per crittografare i dischi virtuali, specificando l'entità servizio di Azure Active Directory e la chiave di crittografia appropriata da usare.</span><span class="sxs-lookup"><span data-stu-id="e2537-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="e2537-156">L'entità servizio di Azure Active Directory richiede la chiave di crittografia necessaria dall'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2537-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="e2537-157">I dischi virtuali vengono crittografati tramite la chiave di crittografia fornita.</span><span class="sxs-lookup"><span data-stu-id="e2537-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="e2537-158">Processo di crittografia</span><span class="sxs-lookup"><span data-stu-id="e2537-158">Encryption process</span></span>
<span data-ttu-id="e2537-159">La crittografia del disco si basa sui componenti aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2537-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="e2537-160">**Insieme di credenziali delle chiavi di Azure**, che consente di proteggere le chiavi crittografiche e private usate per il processo di crittografia/decrittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="e2537-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="e2537-161">Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="e2537-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="e2537-162">Non è necessario dedicare un insieme di credenziali delle chiavi alla crittografia dei dischi.</span><span class="sxs-lookup"><span data-stu-id="e2537-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="e2537-163">Per separare i limiti amministrativi e la visibilità delle chiavi, è possibile creare un insieme di credenziali delle chiavi dedicato.</span><span class="sxs-lookup"><span data-stu-id="e2537-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="e2537-164">**Azure Active Directory** gestisce lo scambio protetto delle chiavi di crittografia necessarie e dell'autenticazione per le azioni richieste.</span><span class="sxs-lookup"><span data-stu-id="e2537-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="e2537-165">In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2537-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="e2537-166">L'entità servizio offre un meccanismo protetto per richiedere e consentire il rilascio delle chiavi di crittografia appropriate.</span><span class="sxs-lookup"><span data-stu-id="e2537-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="e2537-167">Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2537-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="e2537-168">Requisiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="e2537-168">Requirements and limitations</span></span>
<span data-ttu-id="e2537-169">Requisiti relativi alla crittografia dei dischi e scenari supportati:</span><span class="sxs-lookup"><span data-stu-id="e2537-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="e2537-170">I seguenti SKU dei server Linux: Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="e2537-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="e2537-171">Tutte le risorse, come l'insieme di credenziali delle chiavi, l'account di archiviazione e la VM, devono risiedere nella stessa area e nella stessa sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2537-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="e2537-172">VM standard delle serie A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="e2537-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="e2537-173">La crittografia del disco non è attualmente supportata negli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2537-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="e2537-174">VM di base.</span><span class="sxs-lookup"><span data-stu-id="e2537-174">Basic tier VMs.</span></span>
* <span data-ttu-id="e2537-175">VM create con il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e2537-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="e2537-176">Disabilitare la crittografia del disco del sistema operativo nelle VM Linux.</span><span class="sxs-lookup"><span data-stu-id="e2537-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="e2537-177">Aggiornare le chiavi di crittografia in una VM Linux già crittografata.</span><span class="sxs-lookup"><span data-stu-id="e2537-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="e2537-178">Creare le chiavi e l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="e2537-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="e2537-179">È necessario aver installato l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e2537-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="e2537-180">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="e2537-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e2537-181">I nomi dei parametri di esempio includono *myResourceGroup*, *myKey* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="e2537-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="e2537-182">Il primo passaggio consiste nel creare un insieme di credenziali delle chiavi di Azure in cui archiviare le chiavi di crittografia.</span><span class="sxs-lookup"><span data-stu-id="e2537-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="e2537-183">L'insieme di credenziali delle chiavi di Azure consente di archiviare chiavi, chiavi private o password da implementare in tutta sicurezza in applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="e2537-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="e2537-184">Per la crittografia del disco virtuale, usare l'insieme di credenziali delle chiavi per archiviare una chiave di crittografia usata per crittografare o decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="e2537-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="e2537-185">Abilitare il provider dell'insieme di credenziali delle chiavi di Azure nella sottoscrizione di Azure con [az provider register](/cli/azure/provider#register) e creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2537-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e2537-186">L'esempio seguente crea un nome del gruppo di risorse *myResourceGroup* nella posizione `eastus`:</span><span class="sxs-lookup"><span data-stu-id="e2537-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e2537-187">L'insieme di credenziali delle chiavi di Azure contenente le chiavi di crittografia e le risorse di calcolo associate, come l'archiviazione e la VM stessa, devono risiedere nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="e2537-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="e2537-188">Creare un insieme di credenziali delle chiavi di Azure con [az keyvault create](/cli/azure/keyvault#create) e abilitare l'insieme di credenziali delle chiavi per l'utilizzo con crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="e2537-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="e2537-189">Specificare un nome univoco di Key Vault per *keyvault_name* come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2537-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="e2537-190">È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="e2537-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="e2537-191">L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium.</span><span class="sxs-lookup"><span data-stu-id="e2537-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="e2537-192">Esiste un costo aggiuntivo per creare un insieme di credenziali delle chiavi premium, anziché standard, in cui archiviare le chiavi protette tramite software.</span><span class="sxs-lookup"><span data-stu-id="e2537-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="e2537-193">Per creare un insieme di credenziali delle chiavi premium, aggiungere `--sku Premium` al comando del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="e2537-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="e2537-194">L'esempio seguente usa chiavi protette tramite software, poiché viene creato un insieme di credenziali delle chiavi standard.</span><span class="sxs-lookup"><span data-stu-id="e2537-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="e2537-195">Per entrambi i modelli di protezione, è necessario consentire alla piattaforma Azure di accedere all'avvio della VM per richiedere le chiavi di crittografia con cui decrittografare i dischi virtuali.</span><span class="sxs-lookup"><span data-stu-id="e2537-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="e2537-196">Creare una chiave di crittografia nell'insieme di credenziali delle chiavi con [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="e2537-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="e2537-197">Nell'esempio seguente viene creata una chiave denominata *myKey*:</span><span class="sxs-lookup"><span data-stu-id="e2537-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="e2537-198">Creare un'entità servizio di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2537-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="e2537-199">Al momento di crittografare o decrittografare i dischi virtuali, specificare un account per gestisce l'autenticazione e lo scambio delle chiavi di crittografia dall'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="e2537-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e2537-200">Tale account, un'entità servizio di Azure Active Directory, consente alla piattaforma Azure di richiedere le chiavi di crittografia appropriate per conto della VM.</span><span class="sxs-lookup"><span data-stu-id="e2537-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="e2537-201">Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.</span><span class="sxs-lookup"><span data-stu-id="e2537-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="e2537-202">Creare un'entità servizio usando Azure Active Directory con [az ad sp creare-per-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="e2537-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="e2537-203">Nell'esempio seguente vengono letti i valori per l'ID e la password dell'entità servizio per l'uso nei comandi successivi:</span><span class="sxs-lookup"><span data-stu-id="e2537-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="e2537-204">La password viene visualizzata solo quando si crea l'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="e2537-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="e2537-205">Se lo si desidera, visualizzare e registrare la password (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="e2537-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="e2537-206">È possibile elencare le entità servizio con [az ad sp list](/cli/azure/ad/sp#list) e visualizzare informazioni aggiuntive su un'entità servizio specifica con [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="e2537-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="e2537-207">Per crittografare o decrittografare correttamente i dischi virtuali, le autorizzazioni per la chiave di crittografia archiviata nell'insieme di credenziali delle chiavi devono essere impostate in modo tale da consentire all'entità servizio di Azure Active Directory di leggere le chiavi.</span><span class="sxs-lookup"><span data-stu-id="e2537-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="e2537-208">Impostare le autorizzazioni per l'insieme di credenziali delle chiavi con [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="e2537-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="e2537-209">Nell'esempio seguente l'ID dell'entità servizio viene fornita dal comando precedente:</span><span class="sxs-lookup"><span data-stu-id="e2537-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="e2537-210">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e2537-210">Create virtual machine</span></span>
<span data-ttu-id="e2537-211">Per crittografare alcuni dischi virtuali, creare una VM e aggiungere un disco dati.</span><span class="sxs-lookup"><span data-stu-id="e2537-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="e2537-212">Creare una macchina virtuale da crittografare con [az vm create](/cli/azure/vm#create) e collegare un disco dati di 5 Gb.</span><span class="sxs-lookup"><span data-stu-id="e2537-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="e2537-213">Solo determinate immagini di marketplace supportano la crittografia del disco.</span><span class="sxs-lookup"><span data-stu-id="e2537-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="e2537-214">Nell'esempio seguente viene creata una VM denominata *myVM* tramite un'immagine di **CentOS 7.2n**:</span><span class="sxs-lookup"><span data-stu-id="e2537-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="e2537-215">SSH per la macchina virtuale tramite il valore `publicIpAddress` indicato nell'output dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="e2537-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="e2537-216">Creare una partizione e un file system, quindi montare il disco dati.</span><span class="sxs-lookup"><span data-stu-id="e2537-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="e2537-217">Per ulteriori informazioni, vedere [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk) (Connettersi a una VM Linux per montare il nuovo disco).</span><span class="sxs-lookup"><span data-stu-id="e2537-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="e2537-218">Chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="e2537-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="e2537-219">Crittografare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e2537-219">Encrypt virtual machine</span></span>
<span data-ttu-id="e2537-220">Per crittografare i dischi virtuali, è necessario riunire tutti i componenti precedenti:</span><span class="sxs-lookup"><span data-stu-id="e2537-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="e2537-221">Specificare un'entità servizio e la password di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2537-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="e2537-222">Specificare l'insieme di credenziali delle chiavi in cui memorizzare i metadati dei dischi crittografati.</span><span class="sxs-lookup"><span data-stu-id="e2537-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="e2537-223">Specificare le chiavi di crittografia da usare per la crittografia e la decrittografia effettive.</span><span class="sxs-lookup"><span data-stu-id="e2537-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="e2537-224">Specificare se si desidera crittografare il disco del sistema operativo, i dischi dati o tutti i dischi.</span><span class="sxs-lookup"><span data-stu-id="e2537-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="e2537-225">Crittografare la macchina virtuale con [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="e2537-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="e2537-226">Nell'esempio seguente vengono usate le variabili `$sp_id` e `$sp_password` dal comando precedente `ad sp create-for-rbac`:</span><span class="sxs-lookup"><span data-stu-id="e2537-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="e2537-227">Il completamento del processo di crittografia del disco richiede qualche istante.</span><span class="sxs-lookup"><span data-stu-id="e2537-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="e2537-228">Monitorare lo stato del processo con [z vm encryption show](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="e2537-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-229">L'output è simile all'esempio troncato seguente:</span><span class="sxs-lookup"><span data-stu-id="e2537-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="e2537-230">Attendere che lo stato per il sistema operativo del disco indichi **VMRestartPending**, quindi riavviare la macchina virtuale con [az vm restart](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="e2537-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-231">Il processo di crittografia del disco è finalizzato durante il processo di avvio, pertanto, attendere alcuni minuti prima di verificare di nuovo lo stato della crittografia con **az vm encryption show**:</span><span class="sxs-lookup"><span data-stu-id="e2537-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e2537-232">Lo stato dovrebbe ora segnalare sia il disco del sistema operativo che il disco dati come **Crittografato**.</span><span class="sxs-lookup"><span data-stu-id="e2537-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="e2537-233">Aggiungere ulteriori dischi dati</span><span class="sxs-lookup"><span data-stu-id="e2537-233">Add additional data disks</span></span>
<span data-ttu-id="e2537-234">Una volta crittografati i dischi dati, in un secondo momento è possibile aggiungere alla VM ulteriori dischi virtuali e anche crittografarli.</span><span class="sxs-lookup"><span data-stu-id="e2537-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="e2537-235">Ad esempio, consente di aggiungere alla VM un secondo disco virtuale, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2537-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="e2537-236">Eseguire nuovamente il comando per crittografare i dischi virtuali come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e2537-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e2537-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2537-237">Next steps</span></span>
* <span data-ttu-id="e2537-238">Per altre informazioni sulla gestione dell'insieme di credenziali delle chiavi di Azure, tra cui come eliminare chiavi crittografiche e insiemi di credenziali, vedere [Gestire l'insieme di credenziali delle chiavi tramite l'interfaccia della riga di comando](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="e2537-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="e2537-239">Per altre informazioni sulla crittografia del disco, tra cui come preparare una VM personalizzata con crittografia da caricare in Azure, vedere [Crittografia dischi di Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e2537-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
