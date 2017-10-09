---
title: aaaMonitor il dispositivo StorSimple serie 8000 | Documenti Microsoft
description: "Viene descritto come toouse hello dispositivo StorSimple Manager servizio toomonitor utilizzo, le prestazioni dei / o e l'utilizzo della capacità."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Utilizzare toomonitor servizio di gestione di dispositivi StorSimple hello del dispositivo StorSimple
## <a name="overview"></a>Panoramica
È possibile utilizzare dispositivi toomonitor del servizio gestione di dispositivi StorSimple hello specifico all'interno della soluzione StorSimple. È possibile creare grafici personalizzati basati sulle prestazioni, utilizzo della capacità, velocità effettiva della rete e le metriche delle prestazioni di dispositivo i/o e aggiungere tali dashboard toohello. Per ulteriori informazioni, visitare troppo[personalizzare il dashboard del portale](/articles/azure-portal/azure-portal-dashboards.md).

informazioni di monitoraggio hello tooview per un dispositivo specifico, nel portale di Azure hello selezionare il servizio di gestione di dispositivi StorSimple hello. Hello l'elenco di dispositivi, selezionare il dispositivo e quindi andare troppo**monitoraggio**. È quindi possibile visualizzare hello **capacità**, **utilizzo**, e **prestazioni** grafici per dispositivo selezionato hello.

## <a name="capacity"></a>Capacity
**Capacità** tracce hello spazio provisioning e hello restante sul dispositivo hello. la capacità residua Hello viene quindi visualizzato come aggiunto in locale o a livelli.

Hello il provisioning e la capacità residua è ulteriormente suddivisi per i volumi aggiunti in locale e a più livelli. Per ogni volume, hello capacità fornita e hello residua sul dispositivo hello viene visualizzato.

![Capacità I/O](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Utilizzo
**Utilizzo** tiene traccia delle metriche correlate toohello quantità dati spazio di archiviazione utilizzato da hello volumi, contenitori del volume o dispositivo. È possibile creare report in base all'utilizzo delle capacità hello dell'archiviazione primaria, lo spazio di archiviazione cloud o l'archiviazione del dispositivo. L’utilizzo della capacità può essere misurata per un volume specifico, un contenitore del volume specifico o tutti i contenitori del volume.
Per impostazione predefinita, viene segnalato l'utilizzo di hello per le ultime 24 ore. È possibile modificare la durata hello toochange grafico hello su quale hello segnalato l'utilizzo effettuando una selezione da:
* Ultime 24 ore
* Ultimi 7 giorni
* Ultimi 30 giorni
* Ultimi 90 giorni
* Ultimo anno


Hello primario, cloud e archiviazione locale utilizzato può essere descritto di seguito:

### <a name="primary-storage-usage"></a>Uso delle risorse di archiviazione primarie
Questi grafici mostrano quantità hello dei dati scritti tooStorSimple volumi prima di dati hello sono deduplicati e compressi. È possibile visualizzare l'archiviazione primaria di hello usata da tutti i volumi in un contenitore di volumi o per un singolo volume. archiviazione primaria di Hello usata viene ulteriormente suddiviso da primaria a più livelli di archiviazione usato e primario aggiunti in locale l'archiviazione utilizzato.

Hello seguenti grafici mostrano archiviazione primaria di hello utilizzato per un dispositivo StorSimple prima e dopo l'esecuzione di uno snapshot nel cloud. Poiché si tratta solo i dati di volume, uno snapshot nel cloud non dovrebbe modificare archiviazione primaria hello. Come si può notare, hello non mostra alcuna differenza nell'hello aggiunti in locale o a più livelli archiviazione primaria usata in seguito a creare uno snapshot cloud. snapshot cloud Hello avviato circa 11:50 PM nel dispositivo.

![Utilizzo della capacità primario dopo snapshot cloud](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Se è ora eseguire i/o nel dispositivo StorSimple tooyour di hello host connesso, verrà visualizzato un aumento di archiviazione a livelli principale o primario locale aggiunto spazio di archiviazione utilizzato in base al quale volumi (a più livelli o aggiunto in locale) scrivere dati hello. Ecco i grafici relativi all'utilizzo di archiviazione primaria hello per un dispositivo StorSimple. Su questo dispositivo host StorSimple hello avviato l'agente scrive circa 2:30 PM in un volume a più livelli sul dispositivo hello. È possibile vedere punta hello in hello byte/s a scrittura IO toohello in esecuzione in host hello corrispondente.

![Prestazioni durante l'esecuzione I/O su volumi a livelli](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Se si osserva hello a più livelli archiviazione primaria usata, che è diventato backup mentre l'uso di hello primario aggiunto in locale rimane invariato perché sono presenti scritture non servite volumi toohello aggiunto in locale nel dispositivo hello.

![Uso della capacità primaria con I/O eseguiti in volumi a più livelli](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Se si esegue l'aggiornamento 3 o versioni successive, è possibile suddividere utilizzo della capacità di archiviazione primaria hello da un singolo volume, tutti i volumi, tutti i volumi a livelli e tutti i volumi aggiunti in locale come illustrato di seguito. Suddivisione da tutti in locale consentono i volumi aggiunti tooquickly verificare quanta parte del livello locale hello si esaurisca.

![Uso della capacità primaria per tutti i volumi a più livelli](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Utilizzo della capacità primaria per tutti i volumi aggiunti in locale](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Inoltre, è possibile fare clic su ciascuno dei volumi di hello nell'elenco di hello e hello corrispondente utilizzo.

![Utilizzo della capacità primaria per tutti i volumi aggiunti in locale](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Uso dell'archiviazione cloud
Questi grafici mostrano quantità hello di archiviazione cloud usata. Questi dati sono deduplicati e compressi. Questo quantità include snapshot cloud che potrebbero contenere dati che non sono riflessi in nessun volume principale e vengono mantenuti per scopi di legacy o di memorizzazione necessari. È possibile confrontare hello primario e cloud archiviazione consumo figure tooget un'idea di riduzione di dati hello frequenza, anche se il numero di hello non saranno esatto.

Hello seguenti grafici mostrano utilizzo di archiviazione cloud hello di un dispositivo StorSimple quando è stato creato uno snapshot nel cloud.

* snapshot cloud Hello è iniziata alle circa 11:50 am sul dispositivo ed è possibile vedere che prima di snapshot cloud hello, si è verificato alcun archiviazione cloud usata. 
* Una volta snapshot cloud hello completato, utilizzo di spazio di archiviazione cloud hello cattura 0.89 GB. 
* Mentre uno snapshot nel cloud hello era in corso, è inoltre disponibile un picco corrispondente in hello i/o dal dispositivo toocloud.

    ![Uso dell'archiviazione cloud prima dello snapshot cloud](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Uso dell'archiviazione cloud dopo lo snapshot cloud](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![/ O dal dispositivo toocloud durante uno snapshot nel cloud](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Uso dell'archiviazione locale
Questi grafici mostrano l'utilizzo totale di hello per dispositivo hello, che sarà maggiore utilizzo di archiviazione primario perché include un livello di hello SSD lineare. Questo livello contiene una quantità di dati che esista anche nella hello altri livelli del dispositivo. capacità di Hello nel livello di hello SSD lineare viene visualizzato in sequenza in modo che all'arrivo di nuovi dati, dati vecchi hello sono il livello HDD toohello spostato (ora in cui si è deduplicato e compressi) e successivamente toohello cloud.

Nel corso del tempo, archiviazione primario utilizzato e locale di archiviazione utilizzata molto probabilmente aumenterà insieme fino all'iniziano di dati hello toobe a livelli toohello cloud. A questo punto, archiviazione locale di hello utilizzato probabilmente inizierà tooplateau, ma archiviazione primaria di hello usata aumenta man mano che vengono scritti più dati.

Hello seguenti grafici mostrano archiviazione primaria di hello utilizzato per un dispositivo StorSimple quando è stato creato uno snapshot nel cloud. snapshot cloud Hello avviata alle ore 11:50 e archiviazione locale hello avviata diminuendo in quel momento. archiviazione locale di Hello utilizzato arrestato da GB 1.445 too1.09 GB. Indica che probabilmente hello dati non compressi nel livello SSD lineare hello è stati deduplicati compressi e spostati nel livello HDD hello. Si noti che se il dispositivo hello dispone già di una grande quantità di dati sia in unità SSD hello che livelli di unità disco rigido, potrebbe non essere visualizzata questa riduzione. In questo esempio, il dispositivo di hello è una piccola quantità di dati.

![Uso dell'archiviazione locale dopo lo snapshot cloud](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Prestazioni
**Prestazioni** registra le metriche correlate numero toohello di lettura e le operazioni di scrittura tra entrambi iSCSI hello interfacce dell'iniziatore nel server host hello e dispositivo hello o il dispositivo hello e cloud hello. Questa operazione può essere misurata per un volume specifico, un contenitore del volume specifico o tutti i contenitori del volume. Prestazioni includono anche l'utilizzo della CPU e velocità effettiva della rete per hello varie interfacce di rete nel dispositivo.

### <a name="io-performance-for-initiator-toodevice"></a>Prestazioni dei / o per l'iniziatore toodevice
grafico Hello seguente mostra i/o hello per dispositivo di tooyour hello iniziatore per tutti i volumi di hello per un dispositivo di produzione. metriche Hello tracciate sono di lettura e scrittura di byte al secondo. È possibile anche visualizzare un grafico I/O di lettura, scrittura e in attesa o delle latenze di lettura e scrittura.

![Prestazioni dei / o per l'iniziatore toodevice](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Prestazioni dei / o per dispositivo toocloud
Per hello stesso dispositivo, le operazioni dei / o hello vengono tracciate per i dati dal cloud di hello dispositivo toohello hello per tutti i contenitori dei volumi di hello. In questo dispositivo, hello dati solo nel livello lineare hello e non ha distribuito toohello cloud. Non sono presenti operazioni di lettura / scrittura che si verificano dal dispositivo toohello cloud. Pertanto, i picchi nel grafico hello hello sono a un intervallo di 5 minuti corrispondente toohello frequenza con cui viene controllato l'heartbeat hello tra il dispositivo di hello e servizio hello.

Per hello stesso dispositivo, uno snapshot nel cloud è stato usato per i dati di volume avvio alle ore 11:50. Questo ha comportato flusso dal cloud di hello dispositivo toohello dei dati. Operazioni di scrittura sono state soddisfatte cloud toohello tutta la durata. Hello IO grafico mostra un picco hello byte di scrittura/s toohello ora corrispondente quando hello creazione dello snapshot.

![/ O dal dispositivo toocloud durante uno snapshot nel cloud](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Velocità effettiva della rete per le interfacce di rete del dispositivo
**Velocità effettiva della rete** quantità di toohello correlati tiene traccia delle metriche di dati trasferiti dal hello interfacce dell'iniziatore iSCSI rete nel server host di hello dispositivo hello e tra il dispositivo di hello e cloud hello. È possibile monitorare questa metrica per ciascuna delle interfacce di rete iSCSI hello sul dispositivo.

Hello seguenti velocità effettiva della rete hello Mostra grafici per hello Data 0, 1 1 rete GbE nel dispositivo, che sia abilitata per il cloud (impostazione predefinita) e abilitata per iSCSI. In questo dispositivo nel giugno 14 ore circa 9, i dati è stata livelli in cloud hello (nessun cloud in cui sono stati creati snapshot ora quali tootiering punti da hello dati di hello toomove meccanismo in cloud hello) che hanno comportato IO servito toohello cloud. Si è un picco corrispondente nel grafico della velocità effettiva di rete hello per hello stessa ora e la maggior parte del traffico di rete hello è cloud toohello in uscita.

![Velocità effettiva della rete per Data 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Se si esamina grafico velocità effettiva di interfaccia hello Data 1, 1 GbE un'altra rete interfaccia solo è stata abilitata per iSCSI, quindi praticamente alcun traffico di rete non durante tutta la durata.

![Velocità effettiva della rete per Data 1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Utilizzo della CPU per dispositivo
**Utilizzo della CPU** registra le metriche correlate CPU toohello usata nel dispositivo. Hello seguente grafico mostra statistiche di utilizzo della CPU hello per un dispositivo nell'ambiente di produzione.

![Utilizzo della CPU per dispositivo](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[utilizzare dashboard dispositivo del servizio di gestione di dispositivi StorSimple hello](storsimple-device-dashboard.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-manager-service-administration.md).

