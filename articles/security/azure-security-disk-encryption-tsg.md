---
title: risoluzione dei problemi di disco crittografia aaaAzure | Documenti Microsoft
description: Questo articolo offre suggerimenti per la risoluzione dei problemi di Crittografia dischi di Microsoft Azure per VM IaaS Windows e Linux.
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Guida alla risoluzione dei problemi di Crittografia dischi di Azure

Questa guida è per i professionisti IT (IT), informazioni agli analisti della sicurezza e problemi relativi agli amministratori del cloud il cui organizzazioni utilizzano la crittografia del disco di Azure e disco tootroubleshoot materiale sussidiario per la crittografia è necessario.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Risoluzione dei problemi relativi alla crittografia del disco del sistema operativo Linux

Crittografia del disco del sistema operativo Linux è necessario smontare hello del sistema operativo unità precedente toorunning tramite processo di crittografia di hello disco pieno.   Se non è possibile, un messaggio di errore "Impossibile toounmount dopo..." messaggio di errore è probabilmente toooccur.

È molto probabile che ciò si verifichi quando si tenta di eseguire la crittografia del disco del sistema operativo in un ambiente di VM di destinazione che è stato modificato rispetto all'immagine predefinita supportata della raccolta.  Esempi di deviazioni dall'immagine hello è supportato, che può interferire con l'unità di hello del sistema operativo toounmount possibilità dell'estensione hello:
- Immagini personalizzate che non corrispondono più al file system e/o allo schema di partizionamento supportato.
- Immagini personalizzate con applicazioni, ad esempio antivirus, Docker, SAP, MongoDB o Cassandra Apache in esecuzione in tooencryption di hello del sistema operativo precedente.  Queste applicazioni sono tooterminate difficile e quando hanno mantenuto unità toohello del sistema operativo gli handle di file aperti, unità hello non può essere disinstallato, causando un errore.
- Gli script personalizzati eseguiti in chiudono ora passaggio di crittografia di prossimità toohello può interferire e causa questo errore. Questa situazione può verificarsi quando un modello di gestione risorse definisce più estensioni tooexecute contemporaneamente o quando un'estensione script personalizzato o un'altra azione viene eseguita contemporaneamente toodisk crittografia.   La serializzazione e l'isolamento di questi passaggi per risolvere il problema di hello.
- Quando non è stato disabilitato tooenabling precedente crittografia SELinux, hello smontare passaggio si verifica un errore.  È possibile riabilitare SELinux al termine della crittografia.
- Quando il disco del sistema operativo hello utilizza uno schema LVM (anche se il supporto per dischi di dati LVM limitata è disponibile, il disco del sistema operativo LVM non è)
- Requisiti minimi di memoria non soddisfatti. Per la crittografia del disco del sistema operativo sono consigliati 7 GB.
- Montaggio ricorsivo delle unità dati nella directory /mnt/ o l'una nell'altra (ad esempio, /mnt/data1, /mnt/data2, /data3 + /data3/data4 e così via).
- Altri [prerequisiti](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) di Crittografia dischi di Azure per Linux non soddisfatti.

## <a name="unable-tooencrypt"></a>Non è possibile tooencrypt

In alcuni casi, crittografia del disco Linux hello viene toobe bloccata su "Crittografia del disco del sistema operativo avviata" SSH è disabilitata. Questo processo può richiedere tra toocomplete 3-16 ore in un'immagine della raccolta titoli.  Se vengono aggiunti i dischi dati di dimensioni più TB, processo hello potrebbero essere necessari giorni. Hello sequenza di crittografia del disco del sistema operativo Linux Smonta temporaneamente unità hello del sistema operativo ed esegue la crittografia a blocchi dell'intero disco del sistema operativo di hello, prima della reinstallazione nello stato crittografato.   A differenza della crittografia del disco di Azure in Windows, Linux crittografia del disco non utilizzo simultaneo di hello VM mentre la crittografia hello è in corso.  caratteristiche delle prestazioni Hello di hello macchina virtuale, tra cui hello dimensione del disco di hello e se cui account di archiviazione di hello è supportato da archiviazione standard o premium (SSD), possono influenzare notevolmente hello tempi toocomplete crittografia.

stato toocheck, campo ProgressMessage hello restituito da hello [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) comando può essere sottoposto a polling.   Mentre unità hello del sistema operativo viene crittografato hello VM passa allo stato di manutenzione e SSH è inoltre disabilitato tooprevent eventuali interruzioni toohello in corso.  EncryptionInProgress verranno segnalate per la maggior parte di hello del tempo di hello mentre la crittografia è in corso, seguito diverse ore in un secondo momento con un messaggio di VMRestartPending richiesta hello toorestart macchina virtuale.  ad esempio:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Una volta richiesto tooreboot hello VM e dopo il riavvio di hello VM e, offrendo 2-3 minuti per il riavvio di hello e per i passaggi finali toobe eseguita sulla destinazione hello, hello messaggio di stato indicherà che la crittografia infine è stata completata.   Dopo questo messaggio è disponibile, unità del sistema operativo crittografato hello è previsto toobe pronto per l'utilizzo e per hello VM toobe utilizzabile.

Nei casi in cui questa sequenza non è stata individuata, o se le informazioni di avvio, il messaggio di stato di avanzamento o altri indicatori di errore segnalano che la crittografia del sistema operativo non è riuscito il centro di hello del processo (ad esempio se viene visualizzato l'errore "Impossibile toounmount" hello descritti in questa Guida) è consigliabile toorestore hello VM toohello indietro snapshot o backup eseguito tooencryption immediatamente precedente.  Tentativo successivo toohello precedente, è consigliato toore-valutare le caratteristiche di hello di hello macchina virtuale e verificare che tutti i prerequisiti vengono soddisfatti.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Risoluzione dei problemi di Crittografia dischi di Azure dietro un firewall
Quando la connettività è limitata in base alla possibilità di hello un firewall, proxy requisito o impostazioni di gruppo () di sicurezza di rete, di hello estensione tooperform necessarie attività possono essere interrotte.   Ciò può generare messaggi di stato, ad esempio "Stato di estensione non disponibile in VM hello" e gli scenari di errore toofinish.  Nelle sezioni successive Hello presenta alcuni problemi di firewall comuni che è possibile esaminare.

### <a name="network-security-groups"></a>Gruppi di sicurezza di rete
Le impostazioni di gruppo di sicurezza di rete applicate devono consentire ancora configurazione di rete di hello endpoint toomeet hello documentato [prerequisiti](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) per la crittografia del disco.

### <a name="azure-keyvault-behind-firewall"></a>Azure Key Vault dietro un firewall
Hello VM deve essere in grado di tooaccess insieme di credenziali chiave. Fare riferimento tooguidance su errore di accesso tookey da dietro un firewall è gestito da hello [insieme di credenziali chiave](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) team.

### <a name="linux-package-management-behind-firewall"></a>Gestione pacchetti Linux dietro un firewall
In fase di esecuzione, la crittografia del disco di Azure per Linux si basa sulla crittografia tooenabling precedente della distribuzione di destinazione hello pacchetto management system tooinstall necessita componenti dei prerequisiti.  Se le impostazioni del firewall hello VM impediscono toodownload in grado di installare questi componenti, sono previsti errori successivi.    Questo può variare da distribuzione tooconfigure di passaggi di Hello.  In Red Hat, quando è necessario un proxy è essenziale verificare che subscription-manager e yum siano configurati correttamente.  Vedere [questo](https://access.redhat.com/solutions/189533) articolo del supporto Red Hat sull'argomento.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Risoluzione dei problemi di Server Core di Windows Server 2016

In Server Core di Windows Server 2016, il componente di bdehdcfg hello non è disponibile per impostazione predefinita. Questa componente è necessaria per la Crittografia dischi di Azure.

tooworkaround questo problema, hello copia i seguenti 4 file da una cartella di c:\windows\system32 toohello VM di Windows Server 2016 Data Center dell'immagine Server Core di hello:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Eseguire quindi il comando seguente hello:

```
bdehdcfg.exe -target default
```

Verrà creata una partizione di sistema 550MB e quindi dopo un riavvio, è possibile usare Diskpart toocheck hello volumi e continuare.  

ad esempio:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso ulteriori informazioni su alcuni problemi comuni di crittografia del disco di Azure e come tootroubleshoot. Per altre informazioni su questo servizio e sulle relative funzionalità, vedere:

- [Applicare la crittografia dei dischi nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Crittografare una macchina virtuale di Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Crittografia dei dati inattivi di Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
