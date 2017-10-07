---
title: aaaMonitor dispositivo StorSimple | Documenti Microsoft
description: "Viene descritto come toouse hello toomonitor i/o le prestazioni del servizio StorSimple Manager, utilizzo della capacità, velocità effettiva della rete e le prestazioni del dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Utilizzare toomonitor servizio StorSimple Manager di hello del dispositivo StorSimple
## <a name="overview"></a>Panoramica
È possibile utilizzare dispositivi toomonitor del servizio StorSimple Manager hello specifico all'interno della soluzione StorSimple. È possibile creare grafici personalizzati basati su prestazioni I/O, utilizzo della capacità, velocità effettiva della rete e metriche delle prestazioni del dispositivo. 

hello tooview informazioni per un dispositivo specifico, in hello portale di Azure classico, servizio StorSimple Manager selezionare hello di monitoraggio. Fare clic su hello **monitoraggio** scheda e quindi selezionare dall'elenco di hello dei dispositivi. Hello **monitoraggio** pagina contiene le seguenti informazioni hello.

## <a name="io-performance"></a>Prestazione I/O
**Prestazioni dei / o** registra le metriche correlate numero toohello di lettura e le operazioni di scrittura tra entrambi iSCSI hello interfacce dell'iniziatore nel server host hello e dispositivo hello o il dispositivo hello e cloud hello. Questa operazione può essere misurata per un volume specifico, un contenitore del volume specifico o tutti i contenitori del volume.

grafico Hello seguente mostra i/o hello per dispositivo di tooyour hello iniziatore per tutti i volumi di hello per un dispositivo di produzione. metriche Hello tracciate vengono letti e scrivere byte al secondo, leggere e scrivere le operazioni dei / o al secondo, leggere e scrivere le latenze.

![Prestazioni dei / o dall'iniziatore toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Per hello stesso dispositivo, le operazioni dei / o hello vengono tracciate per i dati dal cloud di hello dispositivo toohello hello per tutti i contenitori dei volumi di hello. In questo dispositivo, hello dati solo nel livello lineare hello e non ha distribuito toohello cloud. Non sono presenti operazioni di lettura / scrittura che si verificano dal dispositivo toohello cloud. Pertanto, i picchi nel grafico hello hello sono a un intervallo di 5 minuti corrispondente toohello frequenza con cui viene controllato l'heartbeat hello tra il dispositivo di hello e servizio hello. 

![Prestazioni dei / o dal dispositivo toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Per hello stesso dispositivo, uno snapshot nel cloud è stato usato per i dati di volume a partire da 2:00 pm. Questo ha comportato flusso dal cloud di hello dispositivo toohello dei dati. Operazioni di lettura e scrittura sono state soddisfatte cloud toohello tutta la durata. Hello i/o nel grafico vengono visualizzate un picco hello diverse metriche corrispondente ora toohello snapshot quando hello. 

![Prestazioni dei / o per dispositivo toocloud dopo uno snapshot nel cloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Utilizzo della capacità
**Utilizzo della capacità** tiene traccia delle metriche correlate toohello quantità dati spazio di archiviazione utilizzato da hello volumi, contenitori del volume o dispositivo. È possibile creare report in base all'utilizzo delle capacità hello dell'archiviazione primaria, lo spazio di archiviazione cloud o l'archiviazione del dispositivo. L’utilizzo della capacità può essere misurata per un volume specifico, un contenitore del volume specifico o tutti i contenitori del volume.

Hello primario, cloud e capacità di archiviazione del dispositivo può essere descritto di seguito:

### <a name="primary-storage-capacity-utilization"></a>Utilizzo della capacità di archiviazione primaria
Questi grafici mostrano quantità hello dei dati scritti tooStorSimple volumi prima di dati hello sono deduplicati e compressi. È possibile visualizzare l'uso dell'archiviazione primaria hello da tutti i volumi o per un singolo volume.

Quando si visualizzano hello archiviazione primaria volume utilizzo grafici di capacità per tutti i volumi e i singoli volumi hello e la somma dei dati primaria hello in entrambi i casi, potrebbe esserci una mancata corrispondenza tra due numeri hello. Totale dati primario Hello in tutti i volumi potrebbero non essere sommati toohello somma totale dei dati primaria hello di singoli volumi hello. Questo potrebbe essere dovuto tooone seguenti hello:

* **Dati dello snapshot inclusi per tutti i volumi**: questo comportamento si verifica solo se si esegue una versione precedente all'aggiornamento 3. dati primari di Hello visualizzati per tutti i volumi di hello sono Somma hello di hello di dati primario per ogni volume e hello snapshot. dati primari di Hello visualizzati per un determinato volume corrisponde quantità hello tooonly dati allocati nel volume hello (e non include dati di snapshot del volume corrispondente hello).
  
    Questo può essere spiegato da hello seguente equazione:
  
    *Dati primari (tutti i volumi) = Somma (dati primari (volume i) + dimensioni dei dati dello snapshot (volume i) )*
  
    *WHERE, dati primario (volume i) = dimensioni di dati primario allocati toovolume i*
  
    Se vengono eliminati gli snapshot di hello tramite servizio hello, l'eliminazione di hello viene eseguita in modo asincrono in background hello. Potrebbe richiedere del tempo hello volume dati dimensioni toobe aggiornato dopo l'eliminazione di snapshot hello. 
  
    Se l'esecuzione di Update 3 o versione successiva, non i dati di snapshot hello sono incluso nei dati di volume hello. E l'utilizzo primario hello viene calcolata come segue:
  
    *Dati primari (tutti i volumi) = Somma (dati primari (volume i)
  
    *WHERE, dati primario (volume i) = dimensioni di dati primario allocati toovolume i*
* **Volumi con il monitoraggio disabilitato inclusi in tutti i volumi**: se si dispone di volumi nel dispositivo per cui il monitoraggio è disattivato, dati di monitoraggio di questi singoli volumi hello non sarà disponibile nei grafici hello. Tuttavia, i dati di hello per tutti i volumi nel grafico hello includono volumi hello per cui il monitoraggio è disattivato. 
* **Eliminare i volumi con in tempo reale dei backup associati inclusi per tutti i volumi**: se i volumi contenenti i dati dello snapshot vengono eliminati ma snapshot hello associata ancora esista, quindi è possibile visualizzare una mancata corrispondenza.
* **Volumi eliminati inclusi per tutti i volumi**: In alcuni casi, potrebbero essere presenti volumi precedenti anche se questi sono stati eliminati. effetto Hello di eliminazione non viene visualizzato e il dispositivo hello risulti inferiore capacità disponibile. È necessario toocontact supporto Microsoft tooremove questi volumi.

Hello seguenti grafici mostrano hello archiviazione primaria la capacità di utilizzo di un dispositivo StorSimple prima e dopo l'esecuzione di uno snapshot nel cloud. Poiché si tratta solo i dati di volume, uno snapshot nel cloud non dovrebbe modificare archiviazione primaria hello. Come si può notare, hello non mostra alcuna differenza nell'utilizzo della capacità primario hello in seguito a creare uno snapshot cloud. snapshot cloud Hello avviata in circa 2:00 del dispositivo.

![Utilizzo della capacità primario prima snapshot cloud](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Utilizzo della capacità primario dopo snapshot cloud](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Se si esegue l'aggiornamento 2 o versioni successive, è possibile suddividere utilizzo della capacità di archiviazione primaria hello da un singolo volume, tutti i volumi, tutti i volumi a livelli e tutti i volumi aggiunti in locale come illustrato di seguito. Suddivisione da tutti in locale consentono i volumi aggiunti tooquickly verificare quanta parte del livello locale hello si esaurisca.

![Utilizzo della capacità primaria per tutti i volumi aggiunti in locale](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Utilizzo della capacità di archiviazione cloud
Questi grafici mostrano quantità hello di archiviazione cloud usata. Questi dati sono deduplicati e compressi. Questo quantità include snapshot cloud che potrebbero contenere dati che non sono riflessi in nessun volume principale e vengono mantenuti per scopi di legacy o di memorizzazione necessari. È possibile confrontare hello primario e cloud archiviazione consumo figure tooget un'idea di riduzione di dati hello frequenza, anche se il numero di hello non saranno esatto. Hello seguenti grafici mostrano hello cloud archiviazione la capacità di utilizzo di un dispositivo StorSimple prima e dopo l'esecuzione di uno snapshot nel cloud. Hello snapshot nel cloud è iniziata alle circa 2:00 del dispositivo ed è possibile visualizzare l'utilizzo della capacità cloud hello è aumentato fino al hello stesso tempo, crescente da MB 5.73 too4.04 GB.

![Utilizzo della capacità cloud prima snapshot cloud](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Utilizzo della capacità cloud dopo snapshot cloud](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Utilizzo della capacità di archiviazione del dispositivo
Questi grafici mostrano l'utilizzo totale di hello per dispositivo hello, che sarà maggiore spazio di archiviazione primario perché include un livello di hello SSD lineare. Questo livello contiene una quantità di dati che esista anche nella hello altri livelli del dispositivo. capacità di Hello nel livello di hello SSD lineare viene visualizzato in sequenza in modo che all'arrivo di nuovi dati, dati vecchi hello sono il livello HDD toohello spostato (ora in cui si è deduplicato e compressi) e successivamente toohello cloud.

Nel corso del tempo, l'utilizzo della capacità primario e l'utilizzo della capacità dispositivo molto probabilmente aumenterà insieme fino all'iniziano di dati hello toobe a livelli toohello cloud. A questo punto, l'utilizzo della capacità dispositivo hello probabilmente inizierà tooplateau, ma l'utilizzo della capacità primario hello aumenta man mano che vengono scritti più dati.

Hello seguenti grafici mostrano hello archiviazione primaria la capacità di utilizzo di un dispositivo StorSimple prima e dopo l'esecuzione di uno snapshot nel cloud. snapshot cloud Hello è iniziata alle 2:00 pm e utilizzo della capacità di hello dispositivo avviato diminuendo in quel momento. utilizzo della capacità di archiviazione dispositivo Hello arrestato da GB 11.58 too7.48 GB. Indica che probabilmente hello dati non compressi nel livello SSD lineare hello è stati deduplicati compressi e spostati nel livello HDD hello. Si noti che se il dispositivo hello dispone già di una grande quantità di dati sia in unità SSD hello che livelli di unità disco rigido, potrebbe non essere visualizzata questa riduzione. In questo esempio, il dispositivo di hello è una piccola quantità di dati.

![Utilizzo della capacità di dispositivo prima di snapshot cloud](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Utilizzo della capacità di dispositivo dopo snapshot cloud](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Velocità effettiva della rete
**Velocità effettiva della rete** quantità di toohello correlati tiene traccia delle metriche di dati trasferiti dal hello interfacce dell'iniziatore iSCSI rete nel server host di hello dispositivo hello e tra il dispositivo di hello e cloud hello. È possibile monitorare questa metrica per ciascuna delle interfacce di rete iSCSI hello sul dispositivo.

Hello seguenti velocità effettiva della rete hello Mostra grafici per hello Data 0 e 4 di dati, entrambe le interfacce di rete 1 GbE nel dispositivo. In questo caso, dati 0 è stato abilitato al cloud mentre 4 dati è stata abilitate per iSCSI. È possibile visualizzare entrambi hello in ingresso e hello il traffico in uscita per il dispositivo StorSimple. retta Hello grafico hello a partire dal 3:24 pm è dovuti toohello fatto che è raccogliere i dati solo ogni 5 minuti e deve essere ignorati. 

![Velocità effettiva della rete per Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Velocità effettiva della rete per Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Prestazioni del dispositivo
**Le prestazioni del dispositivo** registra le metriche correlate toohello delle prestazioni del dispositivo. Hello seguente grafico mostra statistiche di utilizzo della CPU hello per un dispositivo nell'ambiente di produzione.

![Utilizzo della CPU per dispositivo](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare dashboard dispositivo del servizio StorSimple Manager hello](storsimple-device-dashboard.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

