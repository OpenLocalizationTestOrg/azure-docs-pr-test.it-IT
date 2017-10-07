---
title: 'Backup di Azure: ripristinare file e cartelle da un backup di VM di Azure | Microsoft Docs'
description: Ripristinare i file da un punto di ripristino della macchina virtuale di Azure
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: ripristino a livello di elemento; ripristino di file da un backup di VM di Azure; ripristinare file da VM di Azure
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Ripristinare i file da un backup della macchina virtuale di Azure

Backup di Azure offre hello funzionalità toorestore [macchine virtuali di Azure e i dischi](./backup-azure-arm-restore-vms.md) da backup di macchina virtuale di Azure. Questo articolo illustra come è possibile ripristinare elementi, come file e cartelle, da un backup di VM di Azure.

> [!Note]
> Questa funzionalità è disponibile per le macchine virtuali di Azure distribuiti tramite il modello di gestione risorse hello e protetto tooa archivio di servizi di ripristino.
> Il ripristino di file da un backup della VM crittografato non è supportato.
>

## <a name="mount-hello-volume-and-copy-files"></a>Montare hello volume e copia i file

1. Sign in hello [portale di Azure](http://portal.Azure.com). Trovare hello rilevanti Recovery services insieme di credenziali e backup dell'elemento hello necessario.

2. Nel Pannello di elemento di Backup hello, fare clic su **ripristino di File**

    ![Aprire la voce di backup dell'insieme di credenziali di Servizi di ripristino](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Hello **ripristino File** apre blade.

    ![Pannello Ripristino file](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Da hello **selezionare il punto di ripristino** dal menu a discesa, un punto di ripristino selezionare hello che contiene file hello desiderato. Per impostazione predefinita, il punto di ripristino più recente hello è già selezionato.

4. Fare clic su **scaricare eseguibile** (per la macchina virtuale Windows Azure) o **Download Script** (per la macchina virtuale di Azure Linux) software hello toodownload che userai toocopy file hello punto di ripristino.

  file eseguibile o script Hello crea una connessione tra computer locali hello e hello specificato punto di ripristino.

5. È necessario un password toorun hello scaricato script o file eseguibile. È possibile copiare la password di hello dal portale di hello con accanto alla copia hello password hello generato

    ![Password generata](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Nel computer in cui si desidera file hello toorecover hello eseguire hello eseguibile o lo script. È necessario eseguire il file eseguibile/script con le credenziali di amministratore. Se si esegue uno script hello in un computer con accesso limitato, verificare l'accesso a è:

    - download.microsoft.com
    - Endpoint di Azure usati per i backup di VM di Azure
    - porta in uscita 3260

   Per Linux, script hello richiede componenti 'open-iscsi' e 'lshw' tooconnect toohello punto di ripristino. Se non quelli esistenti nel computer di hello in cui viene eseguito, richiesto per componenti in questione autorizzazione tooinstall hello e li installa al consenso.
   
   Immettere la password di hello copiata dal portale di hello quando richiesto. Dopo avere immesso la password valida hello script hello si connette il punto di ripristino toohello.
      
    ![Pannello Ripristino file](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   È possibile eseguire script hello in tutti i computer con sistema operativo hello stesso (o compatibile) come backup hello macchina virtuale. Vedere hello [tabella del sistema operativo compatibile](backup-azure-restore-files-from-vm.md#compatible-os) per sistemi operativi compatibili. Se hello protetto virtuale di Azure Usa macchina in che spazi di archiviazione di Windows (per le macchine virtuali di Windows Azure) o Arrays(for Linux VMs) LVM/RAID, sarà possibile eseguire hello eseguibile o lo script hello stessa macchina virtuale. Eseguirlo invece in qualsiasi altro computer con un sistema operativo compatibile.

### <a name="compatible-os"></a>Sistema operativo compatibile

#### <a name="for-windows"></a>Per Windows

Hello nella seguente tabella mostra hello compatibilità tra i sistemi operativi server e computer. Quando si esegue il ripristino dei file, non è possibile ripristinare i file tra sistemi operativi non compatibili.

|Sistema operativo del server | Sistema operativo compatibile del client  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Per Linux

In Linux, requisito fondamentale hello è tale hello del sistema operativo della macchina hello in cui viene eseguito uno script hello deve supportare filesystem hello di hello file presenti nella hello backup VM Linux. Durante la selezione di uno script di hello toorun macchina, verificare che come indicato nella tabella hello riportata di seguito contiene versioni del sistema operativo e hello compatibili hello.

|Sistema operativo Linux | Versioni  |
| --------------- | ---- |
| Ubuntu | 12.04 e versioni successive |
| CentOS | 6.5 e versioni successive  |
| RHEL | 6.7 e versioni successive |
| Debian | 7 e versioni successive |
| Oracle Linux | 6.4 e versioni successive |

script Hello inoltre richiede python e bash tooexecute componenti e connettersi in modo sicuro toohello punto di ripristino.

|Componente | Versione  |
| --------------- | ---- |
| bash | 4 e versioni successive |
| python | 2.6.6 e versioni successive  |


### <a name="identifying-volumes"></a>Identificazione dei volumi

#### <a name="for-windows"></a>Per Windows

Quando si esegue l'eseguibile hello, sistema operativo hello hello nuovi volumi montati e assegna le lettere di unità. È possibile utilizzare Esplora risorse o Esplora File toobrowse tali unità. Hello lettere di unità assegnate toohello volumi potrebbero non essere hello stesse lettere come hello macchina virtuale originale, tuttavia, hello il nome del volume viene mantenuta. Ad esempio, se hello volume nella macchina virtuale originale hello era "disco dati (e:\)", che può essere collegato come volume "disco dati ('Qualsiasi lettera di unità disponibile':\) nel computer locale hello. Esplorare tutti i volumi indicati nell'output di hello dello script fino a individuare il file/cartella.  
       
   ![Pannello Ripristino file](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Per Linux

In Linux, volumi hello hello del punto di ripristino sono montati toohello cartella in cui viene eseguito uno script hello. Hello collegati dischi, volumi e montaggio corrispondente hello percorsi sono visualizzati di conseguenza. Questi percorsi di montaggio sono visibili toousers con accesso al livello radice. Esplorare i volumi di hello indicati nell'output di hello script.

  ![Pannello Ripristino file per Linux](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Chiusura della connessione hello

Dopo aver identificato i file hello e copiarli tooa posizione di archiviazione locale, rimuovere o smontare unità aggiuntive hello. toounmount hello unità, hello **ripristino File** fare clic su pannello nel portale di Azure hello **smontare dischi**.

![Smontare i dischi](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Una volta dischi hello sono stati smontati, viene visualizzato un messaggio per comunicarti che ha avuto esito positivo. Potrebbe richiedere alcuni minuti per toorefresh connessione hello in modo che sia possibile rimuovere i dischi di hello.

In Linux, dopo il punto di ripristino toohello hello connessione viene interrotta, hello del sistema operativo non rimuove i percorsi di montaggio corrispondente hello automaticamente. Vengono forniti come volumi "orfano" e sono visibili, ma verrà generato un errore quando si file hello accesso/scrittura. Questi percorsi possono essere rimossi manualmente. script di Hello, quando eseguito, identifica tali volumi esistenti da punti di ripristino precedente e pulisce al consenso.

## <a name="special-configurations"></a>Configurazioni speciali

### <a name="dynamic-disks"></a>Dischi dinamici

Se hello macchina virtuale di Azure che è stato eseguito il backup di volumi che si estendono su più dischi (volumi con spanning e con striping) e/o a tolleranza di errore (volumi con mirroring e RAID-5) nei dischi dinamici non è possibile eseguire uno script eseguibile hello hello stessa macchina virtuale. Al contrario, eseguire uno script eseguibile hello in qualsiasi altro computer con un sistema operativo compatibile.

### <a name="windows-storage-spaces"></a>Spazi di archiviazione di Windows

Spazi di archiviazione di Windows è una tecnologia di archiviazione di Windows che consente l'archiviazione toovirtualize. Con spazi di archiviazione di Windows è possibile raggruppare dischi standard del settore in pool di archiviazione e quindi creare dischi virtuali, detti spazi di archiviazione dallo spazio disponibile di hello in tali pool di archiviazione.

Se hello macchina virtuale di Azure che è stato eseguito il backup Usa spazi di archiviazione di Windows, quindi è possibile eseguire uno script eseguibile hello in hello stessa macchina virtuale. Al contrario, eseguire uno script eseguibile hello in qualsiasi altro computer con un sistema operativo compatibile.

### <a name="lvmraid-arrays"></a>LVM/matrici RAID

In Linux, il gestore di volumi logici (LVM) e/o software nelle matrici RAID sono volumi logici toomanage usato su più dischi. Se il backup di VM Linux hello utilizza LVM e/o nelle matrici RAID, è possibile eseguire script hello in hello stessa macchina virtuale. Invece di eseguire script hello in qualsiasi altro computer con sistema operativo compatibile e che supporta file System del backup di VM hello.

output di Hello script Visualizza hello LVM e/o i dischi nelle matrici RAID e volumi hello con tipo di partizione hello come illustrato di seguito

   ![Pannello dell'output LVM per Linux](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Hello seguenti comandi necessario toobe eseguire da hello utente toobring queste partizioni online. 

**Per le partizioni LVM**

```
$ pvs <volume name as shown above in hello script output> 
```
Elenca i nomi dei gruppi di volumi hello in un volume fisico.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Elenca tutti i volumi logici, i nomi e i relativi percorsi in un gruppo di volumi.

```
$ mount <LV path> </mountpath>
```
toomount percorso toohello hello volumi logici di propria scelta.


**Per le matrici RAID**

```
$ mdadm –detail –scan
```
Consente di visualizzare informazioni dettagliate su tutti i dischi RAID. verranno visualizzato come disco RAID rilevante Hello`/dev/mdm/<RAID array name in hello backed up VM>`

Utilizzare il comando di montaggio hello se dispone di dischi RAID hello volumi fisici.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Se il disco RAID dispone di un altro LVM configurate Segui hello stessa procedura descritta sopra per le partizioni LVM con il nome del volume hello Nome disco RAID hello

## <a name="troubleshooting"></a>Risoluzione dei problemi

Se si verificano problemi durante il recupero di file di macchine virtuali hello, controllare hello per ulteriori informazioni nella tabella seguente.

| Messaggio di errore/scenario | Possibile causa | Azione consigliata |
| ------------------------ | -------------- | ------------------ |
| Output exe: *eccezione toohello destinazione connessione* |Script non è in grado di tooaccess hello punto di ripristino | Controllare se il computer hello soddisfa i requisiti di accesso hello indicati in precedenza|  
|   Output exe: *destinazione hello è già stato registrato tramite una sessione ISCSI.* |   script Hello già è stato eseguito nella stessa macchina e hello le unità sono state allegate hello |   volumi Hello hello del punto di ripristino sono già stati associati. NON può essere montati con hello stessa unità di hello macchina virtuale originale. Esplorare tutti i volumi disponibili hello in Esplora file hello per il file |
| Output exe: *questo script non è valido perché è necessario smontare dischi hello attraverso il limite di 12 ore hello portale/superato. Scaricare un nuovo script dal portale hello.* |    è necessario smontare dischi Hello dal portale di hello o superato il limite di hello 12 ore |  Non è possibile eseguire questo specifico file con estensione exe perché non è più valido. Se si desidera tooaccess hello i file di tale ripristino punto nel tempo, visitare il portale di hello per un nuovo file exe|
| Nel computer di hello in cui viene eseguito exe hello: nuovi volumi hello non vengono smontati dopo hello lo smontaggio del pulsante |    iniziatore ISCSI Hello computer hello non risponde/aggiornare la destinazione toohello di connessione e la gestione di cache di hello |    Attendere alcuni minuti dopo hello lo smontaggio del pulsante. Se i nuovi volumi hello non sono ancora disinstallati, passare attraverso tutti i volumi di hello. Questo viene smontato hello iniziatore toorefresh hello connessione hello volume e con un messaggio di errore di forza che hello disco non è disponibile|
| Output exe: Script è stato eseguito correttamente ma "Nuovi volumi collegati" non sono visualizzati nell'output di hello script |   Si tratta di un errore temporaneo   | volumi Hello potrebbero aver già allegati. Aprire Esplora toobrowse. Se si utilizza hello stesso computer per l'esecuzione di script ogni volta, si consiglia di riavviare il computer hello e hello elenco deve essere visualizzato nelle esecuzioni successive exe hello. |
| Specifiche di Linux: non è possibile tooview hello desiderato volumi | Hello del sistema operativo della macchina hello in cui viene eseguito uno script hello potrebbe non riconoscere hello filesystem sottostante di hello backup VM | Verifica se il punto di ripristino hello è l'arresto anomalo del sistema coerente o coerenti con i file. Se lo script in un altro computer il cui sistema operativo riconosce hello hello coerente, l'esecuzione del file di backup del file System della macchina virtuale |
| Specifiche di Windows: non è possibile tooview hello desiderato volumi | dischi Hello collegati ma non sono stati configurati i volumi di hello | Dalla schermata di Gestione disco hello, identificare un punto di ripristino correlati toohello hello dischi aggiuntivi. Se uno di questi dischi è non in linea in stato di provare a renderli online facendo clic sul disco hello e fare clic su 'In linea'|
