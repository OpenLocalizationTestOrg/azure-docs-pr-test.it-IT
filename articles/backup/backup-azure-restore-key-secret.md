---
title: Ripristinare la chiave dell'insieme di credenziali delle chiavi e il segreto per le macchine virtuali crittografate con Backup di Azure | Documentazione Microsoft
description: Informazioni su come ripristinare la chiave dell'insieme di credenziali delle chiavi e il segreto in Backup di Azure usando PowerShell
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="65691-103">Ripristinare la chiave dell'insieme di credenziali delle chiavi e il segreto per le macchine virtuali crittografate con Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="65691-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="65691-104">Questo articolo illustra l'uso di Backup di Azure per eseguire il ripristino delle macchine virtuali crittografate di Azure nel caso in cui la chiave e il segreto non siano presenti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="65691-105">Questa procedura può essere usata anche per conservare una copia separata della chiave (chiave di crittografia della chiave) e del segreto (chiave di crittografia BitLocker) per la macchina virtuale ripristinata.</span><span class="sxs-lookup"><span data-stu-id="65691-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65691-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65691-106">Prerequisites</span></span>
* <span data-ttu-id="65691-107">**Backup delle macchine virtuali crittografate**: il backup delle macchine virtuali crittografate di Azure deve essere eseguito tramite Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="65691-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="65691-108">Per informazioni dettagliate sul backup di macchine virtuali crittografate di Azure, vedere l'articolo relativo alla [gestione del backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="65691-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="65691-109">**Configurazione dell'insieme di credenziali delle chiavi di Azure**: assicurarsi che l'insieme di credenziali delle chiavi in cui eseguire il ripristino di chiavi e segreti sia presente.</span><span class="sxs-lookup"><span data-stu-id="65691-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="65691-110">Per informazioni dettagliate sulla gestione dell'insieme di credenziali delle chiavi, vedere l'articolo [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65691-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="65691-111">**Ripristino del disco**: assicurarsi di aver attivato il processo di ripristino per ripristinare i dischi delle macchine virtuali crittografate usando le [procedure di PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="65691-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="65691-112">Questo processo, infatti, genera un file JSON nell'account di archiviazione contenente le chiavi e i segreti della macchina virtuale crittografata da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="65691-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="65691-113">Ottenere la chiave e il segreto da Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="65691-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="65691-114">Dopo aver ripristinato il disco per la macchina virtuale crittografata, verificare che:</span><span class="sxs-lookup"><span data-stu-id="65691-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="65691-115">In $details siano specificati i dettagli del processo di ripristino del disco, come indicato nella [procedura relativa a PowerShell della sezione Ripristinare i dischi](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="65691-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="65691-116">La macchina virtuale venga creata dai dischi ripristinati solo **dopo aver ripristinato la chiave e il segreto nell'insieme di credenziali delle chiavi**.</span><span class="sxs-lookup"><span data-stu-id="65691-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="65691-117">Ricercare i dettagli del processo nelle proprietà del disco ripristinato.</span><span class="sxs-lookup"><span data-stu-id="65691-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="65691-118">Impostare il contesto di archiviazione di Azure e ripristinare il file di configurazione JSON contenente i dettagli relativi alla chiave e al segreto della macchina virtuale crittografata.</span><span class="sxs-lookup"><span data-stu-id="65691-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="65691-119">Ripristinare la chiave</span><span class="sxs-lookup"><span data-stu-id="65691-119">Restore key</span></span>
<span data-ttu-id="65691-120">Dopo aver generato il file JSON nel percorso di destinazione indicato in precedenza, generare il file BLOB della chiave dal file JSON e compilarlo in modo da ripristinare il cmdlet della chiave e reinserire la chiave di crittografia della chiave (KEK) nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="65691-121">Ripristinare il segreto</span><span class="sxs-lookup"><span data-stu-id="65691-121">Restore secret</span></span>
<span data-ttu-id="65691-122">Usare il file JSON generato in precedenza per ottenere il valore e il nome del segreto e compilarlo in modo da impostare il cmdlet del segreto per reinserire il segreto (BEK) nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="65691-123">**Usare questi cmdlet se la macchina virtuale è crittografata con BEK e KEK.**</span><span class="sxs-lookup"><span data-stu-id="65691-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="65691-124">Se la macchina virtuale è **crittografata solo con BEK**, generare il file di BLOB del segreto dal file JSON e compilarlo in modo da ripristinare il cmdlet del segreto per reinserire il segreto (BEK) nell'insieme di credenziali chiave di ripristino.</span><span class="sxs-lookup"><span data-stu-id="65691-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="65691-125">È possibile ottenere il valore di $secretname facendo riferimento all'output di $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e usando il testo presente dopo secrets/. Se, ad esempio, l'URL del segreto di output è https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163, il nome del segreto sarà B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="65691-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="65691-126">Il valore del tag DiskEncryptionKeyFileName è uguale al nome del segreto.</span><span class="sxs-lookup"><span data-stu-id="65691-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="65691-127">Creare una macchina virtuale dal disco ripristinato</span><span class="sxs-lookup"><span data-stu-id="65691-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="65691-128">Se il backup della macchina virtuale crittografata è stato eseguito tramite Backup di Azure, i cmdlet di PowerShell elencati in precedenza consentono di ripristinare chiave e segreto nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="65691-129">Dopo avere eseguito il ripristino, per creare le macchine virtuali crittografate dal disco, dalla chiave e dal segreto ripristinato, vedere l'articolo relativo alla [gestione del backup e del ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span><span class="sxs-lookup"><span data-stu-id="65691-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="65691-130">Approccio legacy</span><span class="sxs-lookup"><span data-stu-id="65691-130">Legacy approach</span></span>
<span data-ttu-id="65691-131">L'approccio sopra descritto potrà essere adottato per tutti i punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="65691-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="65691-132">L'approccio precedente, che prevedeva di recuperare le informazioni sulla chiave e sul segreto dal punto di ripristino, può essere ancora adottato per i punti di ripristino precedenti all'11 luglio 2017 per le macchine virtuali crittografate con BEK e KEK.</span><span class="sxs-lookup"><span data-stu-id="65691-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="65691-133">Dopo aver completato il processo di ripristino del disco per le macchine virtuali crittografate applicando la [procedura relativa a PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), assicurarsi che in $rp sia inserito un valore valido.</span><span class="sxs-lookup"><span data-stu-id="65691-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="65691-134">Ripristinare la chiave</span><span class="sxs-lookup"><span data-stu-id="65691-134">Restore key</span></span>
<span data-ttu-id="65691-135">Usare i cmdlet seguenti per ottenere informazioni sulla chiave di crittografia della chiave dal punto di ripristino e compilarli in modo da ripristinare il cmdlet della chiave e reinserirlo nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="65691-136">Ripristinare il segreto</span><span class="sxs-lookup"><span data-stu-id="65691-136">Restore secret</span></span>
<span data-ttu-id="65691-137">Usare i cmdlet seguenti per ottenere informazioni sulla chiave di crittografia a blocchi dal punto di ripristino e compilarli in modo da impostare il cmdlet del segreto e reinserirlo nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="65691-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="65691-138">È possibile ottenere il valore di $secretname facendo riferimento all'output di $rp1.KeyAndSecretDetails.SecretUrl e usando il testo presente dopo secrets/. Se, ad esempio, l'URL del segreto di output è https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163, il nome del segreto sarà B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="65691-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="65691-139">Il valore del tag DiskEncryptionKeyFileName è uguale al nome del segreto.</span><span class="sxs-lookup"><span data-stu-id="65691-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="65691-140">È possibile ottenere il valore di DiskEncryptionKeyEncryptionKeyURL dall'insieme di credenziali delle chiavi dopo il ripristino delle chiavi, usando il cmdlet [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx).</span><span class="sxs-lookup"><span data-stu-id="65691-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="65691-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65691-141">Next steps</span></span>
<span data-ttu-id="65691-142">Dopo aver ripristinato la chiave e il segreto nell'insieme di credenziali delle chiavi, vedere l'articolo relativo alla [gestione delle procedure di backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) per creare le macchine virtuali crittografate dal disco, dalla chiave e dal segreto ripristinati.</span><span class="sxs-lookup"><span data-stu-id="65691-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
