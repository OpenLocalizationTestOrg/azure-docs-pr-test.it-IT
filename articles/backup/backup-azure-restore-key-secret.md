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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Ripristinare la chiave dell'insieme di credenziali delle chiavi e il segreto per le macchine virtuali crittografate con Backup di Azure
In questo articolo parla utilizzando Backup di Azure VM tooperform ripristino delle macchine virtuali di Azure crittografato, se la chiave e il segreto non esistono nell'insieme di credenziali chiave hello. Questi passaggi è utilizzabile anche se si desidera toomaintain una copia separata della chiave (Key Encryption Key) e secret (chiave di crittografia di BitLocker) per hello ripristinato macchina virtuale.

## <a name="prerequisites"></a>Prerequisiti
* **Backup delle macchine virtuali crittografate**: il backup delle macchine virtuali crittografate di Azure deve essere eseguito tramite Backup di Azure. Vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md) per informazioni dettagliate su come toobackup crittografati macchine virtuali di Azure.
* **Configurare l'insieme di credenziali chiave di Azure** : verificare che tale insieme di credenziali chiave toowhich chiavi e segreti necessità toobe ripristinato è già presente. Vedere l'articolo hello [introduzione insieme credenziali chiavi Azure](../key-vault/key-vault-get-started.md) per informazioni dettagliate sulla gestione dell'insieme di credenziali chiave.
* **Ripristino del disco**: assicurarsi di aver attivato il processo di ripristino per ripristinare i dischi delle macchine virtuali crittografate usando le [procedure di PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Questo avviene perché questo processo genera un file JSON nell'account di archiviazione contenente le chiavi e segreti per crittografato hello VM toobe ripristinato.

## <a name="get-key-and-secret-from-azure-backup"></a>Ottenere la chiave e il segreto da Backup di Azure

> [!NOTE]
> Una volta per macchina virtuale di crittografato hello, disco è stato ripristinato, verificare quanto segue:
> 1. $details viene popolato con i dettagli dei processi di ripristino su disco, come indicato nella [PowerShell passaggi nella sezione dischi hello di ripristino](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. Macchina virtuale deve essere creato da solo i dischi ripristinati **dopo chiave e il segreto dell'insieme di credenziali tookey ripristinato**.
>
>

Hello query ripristinato proprietà del disco per i dettagli dei processi hello.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Impostare il contesto di archiviazione di Azure hello e ripristinare i file di configurazione JSON contenente colonne chiave e dettagli segreti per la macchina virtuale crittografata.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Ripristinare la chiave
Dopo la generazione del file JSON hello nel percorso di destinazione hello indicato in precedenza, generare file di BLOB della chiave da hello JSON e feed, chiave di hello toorestore cmdlet chiave tooput (KEK) indietro nell'insieme di credenziali chiave hello.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Ripristinare il segreto
Utilizza il file JSON di hello generato in precedenza tooget secret nome e valore e feed il segreto di hello tooset cmdlet secret tooput (BEK) indietro nell'insieme di credenziali chiave di hello. **Usare questi cmdlet se la macchina virtuale è crittografata con BEK e KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Se la macchina virtuale è **crittografati utilizzando solo BEK**, generare file di blob segreto da hello JSON e feed il segreto di hello toorestore cmdlet secret tooput (BEK) indietro nell'insieme di credenziali chiave hello.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Valore per $secretname può essere ottenuto tramite riferimento output toohello di $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e l'utilizzo di testo dopo i segreti / ad esempio output secret URL è https://keyvaultname.vault.azure.net/secrets/ Nome B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e segreto è B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valore del tag hello DiskEncryptionKeyFileName è uguale al nome del segreto.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Creare una macchina virtuale dal disco ripristinato
Se è stato eseguito il backup crittografato macchina virtuale utilizzando il Backup di VM di Azure, hello i cmdlet di PowerShell indicato in precedenza della Guida che si ripristina chiave e l'insieme di credenziali chiave segreta toohello indietro. Dopo il ripristino di questi, vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate crittografato macchine virtuali dal disco ripristinato, chiave e chiave privata.

## <a name="legacy-approach"></a>Approccio legacy
approccio Hello indicato in precedenza funzionerà per tutti i punti di ripristino hello. Tuttavia, hello approccio meno recente di recupero chiave e le informazioni segrete dal punto di ripristino, sarà valido per i punti di ripristino meno recente 11 luglio 2017 per le macchine virtuali crittografate utilizzando BEK e KEK. Dopo aver completato il processo di ripristino del disco per le macchine virtuali crittografate applicando la [procedura relativa a PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), assicurarsi che in $rp sia inserito un valore valido.

### <a name="restore-key"></a>Ripristinare la chiave
Utilizzare le seguenti informazioni chiave (KEK) di cmdlet tooget dal punto di ripristino hello e feed di toorestore cmdlet chiave tooput nuovamente nell'insieme di credenziali chiave hello.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Ripristinare il segreto
Utilizzare le seguenti informazioni di cmdlet tooget segreto (BEK) dal punto di ripristino hello e feed di tooset cmdlet secret tooput nuovamente nell'insieme di credenziali chiave hello.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Valore per $secretname può essere ottenuto tramite un riferimento output toohello di $rp1. KeyAndSecretDetails.SecretUrl e l'utilizzo di testo dopo i segreti / ad esempio output secret URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e segreto nome B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valore del tag hello DiskEncryptionKeyFileName è uguale al nome del segreto.
> 3. Valore per DiskEncryptionKeyEncryptionKeyURL può essere ottenuto dall'insieme di credenziali chiave dopo il ripristino delle chiavi di hello nuovamente e l'utilizzo [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>Passaggi successivi
Dopo il ripristino di chiave e il segreto tookey indietro dell'insieme di credenziali, vedere l'articolo hello [gestire backup e ripristino di macchine virtuali di Azure con PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate crittografato macchine virtuali dal disco ripristinato, chiave e il segreto.
