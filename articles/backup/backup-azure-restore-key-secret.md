---
title: chiave di insieme di credenziali chiave aaaRestore e il segreto per crittografati macchine virtuali con Backup di Azure | Documenti Microsoft
description: Informazioni su come toorestore chiave dell'insieme di credenziali chiave e il segreto in Backup di Azure tramite PowerShell
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
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="2aacd-103">Ripristinare la chiave dell'insieme di credenziali delle chiavi e il segreto per le macchine virtuali crittografate con Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="2aacd-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="2aacd-104">In questo articolo parla utilizzando Backup di Azure VM tooperform ripristino delle macchine virtuali di Azure crittografato, se la chiave e il segreto non esistono nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="2aacd-105">Questi passaggi è utilizzabile anche se si desidera toomaintain una copia separata della chiave (Key Encryption Key) e secret (chiave di crittografia di BitLocker) per hello ripristinato macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2aacd-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aacd-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2aacd-106">Prerequisites</span></span>
* <span data-ttu-id="2aacd-107">**Backup delle macchine virtuali crittografate**: il backup delle macchine virtuali crittografate di Azure deve essere eseguito tramite Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aacd-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="2aacd-108">Vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md) per informazioni dettagliate su come toobackup crittografati macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2aacd-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="2aacd-109">**Configurare l'insieme di credenziali chiave di Azure** : verificare che tale insieme di credenziali chiave toowhich chiavi e segreti necessità toobe ripristinato è già presente.</span><span class="sxs-lookup"><span data-stu-id="2aacd-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="2aacd-110">Vedere l'articolo hello [introduzione insieme credenziali chiavi Azure](../key-vault/key-vault-get-started.md) per informazioni dettagliate sulla gestione dell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="2aacd-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="2aacd-111">**Ripristino del disco**: assicurarsi di aver attivato il processo di ripristino per ripristinare i dischi delle macchine virtuali crittografate usando le [procedure di PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="2aacd-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="2aacd-112">Questo avviene perché questo processo genera un file JSON nell'account di archiviazione contenente le chiavi e segreti per crittografato hello VM toobe ripristinato.</span><span class="sxs-lookup"><span data-stu-id="2aacd-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="2aacd-113">Ottenere la chiave e il segreto da Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="2aacd-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="2aacd-114">Una volta per macchina virtuale di crittografato hello, disco è stato ripristinato, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2aacd-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="2aacd-115">$details viene popolato con i dettagli dei processi di ripristino su disco, come indicato nella [PowerShell passaggi nella sezione dischi hello di ripristino](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="2aacd-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="2aacd-116">Macchina virtuale deve essere creato da solo i dischi ripristinati **dopo chiave e il segreto dell'insieme di credenziali tookey ripristinato**.</span><span class="sxs-lookup"><span data-stu-id="2aacd-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="2aacd-117">Hello query ripristinato proprietà del disco per i dettagli dei processi hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="2aacd-118">Impostare il contesto di archiviazione di Azure hello e ripristinare i file di configurazione JSON contenente colonne chiave e dettagli segreti per la macchina virtuale crittografata.</span><span class="sxs-lookup"><span data-stu-id="2aacd-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="2aacd-119">Ripristinare la chiave</span><span class="sxs-lookup"><span data-stu-id="2aacd-119">Restore key</span></span>
<span data-ttu-id="2aacd-120">Dopo la generazione del file JSON hello nel percorso di destinazione hello indicato in precedenza, generare file di BLOB della chiave da hello JSON e feed, chiave di hello toorestore cmdlet chiave tooput (KEK) indietro nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="2aacd-121">Ripristinare il segreto</span><span class="sxs-lookup"><span data-stu-id="2aacd-121">Restore secret</span></span>
<span data-ttu-id="2aacd-122">Utilizza il file JSON di hello generato in precedenza tooget secret nome e valore e feed il segreto di hello tooset cmdlet secret tooput (BEK) indietro nell'insieme di credenziali chiave di hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="2aacd-123">**Usare questi cmdlet se la macchina virtuale è crittografata con BEK e KEK.**</span><span class="sxs-lookup"><span data-stu-id="2aacd-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="2aacd-124">Se la macchina virtuale è **crittografati utilizzando solo BEK**, generare file di blob segreto da hello JSON e feed il segreto di hello toorestore cmdlet secret tooput (BEK) indietro nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="2aacd-125">Valore per $secretname può essere ottenuto tramite riferimento output toohello di $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e l'utilizzo di testo dopo i segreti / ad esempio output secret URL è https://keyvaultname.vault.azure.net/secrets/ Nome B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e segreto è B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="2aacd-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="2aacd-126">Valore del tag hello DiskEncryptionKeyFileName è uguale al nome del segreto.</span><span class="sxs-lookup"><span data-stu-id="2aacd-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="2aacd-127">Creare una macchina virtuale dal disco ripristinato</span><span class="sxs-lookup"><span data-stu-id="2aacd-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="2aacd-128">Se è stato eseguito il backup crittografato macchina virtuale utilizzando il Backup di VM di Azure, hello i cmdlet di PowerShell indicato in precedenza della Guida che si ripristina chiave e l'insieme di credenziali chiave segreta toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="2aacd-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="2aacd-129">Dopo il ripristino di questi, vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate crittografato macchine virtuali dal disco ripristinato, chiave e chiave privata.</span><span class="sxs-lookup"><span data-stu-id="2aacd-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="2aacd-130">Approccio legacy</span><span class="sxs-lookup"><span data-stu-id="2aacd-130">Legacy approach</span></span>
<span data-ttu-id="2aacd-131">approccio Hello indicato in precedenza funzionerà per tutti i punti di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="2aacd-132">Tuttavia, hello approccio meno recente di recupero chiave e le informazioni segrete dal punto di ripristino, sarà valido per i punti di ripristino meno recente 11 luglio 2017 per le macchine virtuali crittografate utilizzando BEK e KEK.</span><span class="sxs-lookup"><span data-stu-id="2aacd-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="2aacd-133">Dopo aver completato il processo di ripristino del disco per le macchine virtuali crittografate applicando la [procedura relativa a PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), assicurarsi che in $rp sia inserito un valore valido.</span><span class="sxs-lookup"><span data-stu-id="2aacd-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="2aacd-134">Ripristinare la chiave</span><span class="sxs-lookup"><span data-stu-id="2aacd-134">Restore key</span></span>
<span data-ttu-id="2aacd-135">Utilizzare le seguenti informazioni chiave (KEK) di cmdlet tooget dal punto di ripristino hello e feed di toorestore cmdlet chiave tooput nuovamente nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="2aacd-136">Ripristinare il segreto</span><span class="sxs-lookup"><span data-stu-id="2aacd-136">Restore secret</span></span>
<span data-ttu-id="2aacd-137">Utilizzare le seguenti informazioni di cmdlet tooget segreto (BEK) dal punto di ripristino hello e feed di tooset cmdlet secret tooput nuovamente nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="2aacd-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="2aacd-138">Valore per $secretname può essere ottenuto tramite un riferimento output toohello di $rp1. KeyAndSecretDetails.SecretUrl e l'utilizzo di testo dopo i segreti / ad esempio output secret URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e segreto nome B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="2aacd-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="2aacd-139">Valore del tag hello DiskEncryptionKeyFileName è uguale al nome del segreto.</span><span class="sxs-lookup"><span data-stu-id="2aacd-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="2aacd-140">Valore per DiskEncryptionKeyEncryptionKeyURL può essere ottenuto dall'insieme di credenziali chiave dopo il ripristino delle chiavi di hello nuovamente e l'utilizzo [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="2aacd-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2aacd-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2aacd-141">Next steps</span></span>
<span data-ttu-id="2aacd-142">Dopo il ripristino di chiave e il segreto tookey indietro dell'insieme di credenziali, vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate crittografato macchine virtuali dal disco ripristinato, chiave e il segreto.</span><span class="sxs-lookup"><span data-stu-id="2aacd-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
