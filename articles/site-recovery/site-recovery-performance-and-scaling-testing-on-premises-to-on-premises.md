---
title: aaaTest risultati per la replica Hyper-V tra siti con Azure Site Recovery | Documenti Microsoft
description: "Questo articolo fornisce informazioni sui test delle prestazioni per la replica tooon tra più sedi locali delle macchine virtuali Hyper-V usando Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Risultati dei test per la replica Hyper-V tooon tra più sedi locali con il ripristino del sito

È possibile utilizzare Microsoft Azure Site Recovery tooorchestrate e gestire la replica del Data Center secondario tooa e tooAzure server fisici o macchine virtuali. Questo articolo fornisce risultati hello del test delle prestazioni che è stato fatto quando la replica delle macchine virtuali Hyper-V tra due nel data center locali.

## <a name="test-goals"></a>Obiettivi di test

obiettivo di Hello del test è stato tooexamine modalità di funzionamento di Azure Site Recovery durante la replica nello stato stazionario. La replica dello stato stazionario si verifica quando le macchine virtuali hanno completato la replica iniziale e sincronizzano le modifiche differenziali. È importante toomeasure prestazioni usando lo stato stazionario perché è stato hello in cui la maggior parte delle macchine virtuali di rimanere a meno che non si verificano interruzioni impreviste.

distribuzione di prova Hello è costituito da due siti locali con un server VMM in ogni sito. Distribuzione di questo test è tipica di una distribuzione di office sede centrale/filiale, con la sede centrale che funge da sito primario di hello e succursale hello come sito secondario o di ripristino di hello.

## <a name="what-we-did"></a>Passaggi eseguiti

Ecco cosa è in test hello passare:

1. Creare macchine virtuali utilizzando modelli VMM.
2. Avviare le macchine virtuali e acquisire le metriche delle prestazioni di acquisizione dei dati di base per 12 ore.
3. Creare i cloud nei server VMM primario e di ripristino.
4. Configurare la protezione del cloud in Azure Site Recovery, compreso il mapping dei cloud di origine e di ripristino.
5. Abilitare la protezione per le macchine virtuali e consentire loro toocomplete la replica iniziale.
6. Attendere un paio d'ore per la stabilizzazione del sistema.
7. Acquisire le metriche delle prestazioni per 12 ore, assicurandosi che tutte le macchine virtuali rimangano in uno stato di replica previsto per queste 12 ore.
8. Misurare il delta di hello tra le metriche delle prestazioni di base hello e hello le metriche delle prestazioni di replica.


## <a name="primary-server-performance"></a>Prestazioni del server primario

* Replica Hyper-V in modo asincrono tiene traccia delle modifiche tooa file registro con overhead di archiviazione minimo nel server primario hello.
* La Replica Hyper-V Usa la memoria autonoma cache toominimize IOPS overhead per il rilevamento. Archivia le scritture toohello VHDX in memoria e scaricamenti in file di log hello prima hello ora tale registro hello viene inviato il sito di ripristino toohello. Lo scaricamento del disco avviene anche se hello scritture raggiungono un limite predeterminato.
* grafico Hello riportato di seguito viene illustrato l'overhead IOPS hello nello stato stazionario per la replica. Possiamo vedere che hello tooreplication overhead dovuto IOPS è di circa il 5% ovvero abbastanza basso.

![Risultati sito primario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Replica Hyper-V prevede l'utilizzo di memoria sulle prestazioni del disco toooptimize di hello server primario. Come illustrato nel seguente grafico hello, l'overhead della memoria in tutti i server nel cluster primario hello è marginale. Hello overhead della memoria mostrato è percentuale hello di memoria utilizzata dalla replica rispetto toohello totale installata memoria nel server Hyper-V hello.

![Risultati sito primario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Replica Hyper-V ha un sovraccarico di CPU minimo. Come illustrato nel grafico hello, overhead di replica è compreso nell'intervallo di hello di % 2 e 3.

![Risultati sito primario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Prestazioni del server secondario (ripristino)

Replica Hyper-V Usa una piccola quantità di memoria numero hello ripristino server toooptimize hello di operazioni di archiviazione. grafico Hello riepiloga l'utilizzo della memoria hello nel server di ripristino hello. Hello overhead della memoria mostrato è percentuale hello di memoria utilizzata dalla replica rispetto toohello totale installata memoria nel server Hyper-V hello.

![Risultati sito secondario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

quantità di Hello di operazioni dei / o nel sito di ripristino hello è una funzione del numero di hello di operazioni di scrittura nel sito primario di hello. Si esaminerà operazioni dei / o totale di hello nel sito di ripristino hello rispetto al numero di operazioni dei / o totale hello e le operazioni nel sito primario di hello di scrittura. grafici di Hello mostrano il totale di hello che IOPS nel sito di ripristino hello

* IOPS di scrittura di circa 1,5 volte hello in hello primario.
* Circa il 37% della hello totale IOPS nel sito primario di hello.

![Risultati sito secondario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Risultati sito secondario](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Risultati dell'uso di rete

Una media di 275 Mb al secondo di larghezza di banda di rete utilizzata tra hello primario e i nodi di ripristino (con compressione abilitata) con una larghezza di banda esistente di 5 Gb al secondo.

![Risultati utilizzo rete](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Effetto sulle prestazioni della macchina virtuale

Una considerazione importante è l'impatto di hello della replica sui carichi di lavoro di produzione in esecuzione in macchine virtuali hello. Se sito primario di hello è adeguato per la replica, non deve essere presente alcun impatto sui carichi di lavoro hello. Meccanismo di rilevamento a bassa densità della Replica Hyper-V assicura che i carichi di lavoro in esecuzione in macchine virtuali hello non sono interessati durante la replica nello stato stazionario. Come illustrato nel seguente grafici hello.

Questo grafico mostra IOPS eseguiti dalle macchine virtuali con carichi di lavoro diversi prima e dopo l'abilitazione della replica. È possibile osservare che non vi è alcuna differenza tra due hello.

![Risultati effetto replica ](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Hello seguente grafico mostra la velocità effettiva hello di macchine virtuali che eseguono carichi di lavoro diversi prima e dopo l'abilitazione della replica. È possibile osservare che la replica non ha alcun impatto significativo.

![Risultati effetti replica ](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Conclusioni

risultati di Hello indicano chiaramente che Azure Site Recovery, insieme con Replica Hyper-V, è scalabile con overhead minimo per un cluster di grandi dimensioni.  Azure Site Recovery consente di eseguire in modo semplice distribuzione, replica, gestione e monitoraggio. Replica Hyper-V fornisce l'infrastruttura necessaria hello per ridimensionare il completamento della replica. Per la pianificazione di una distribuzione ottimale, è consigliabile scaricare hello [Hyper-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Ambiente di test nel dettaglio

### <a name="primary-site"></a>Sito primario

* sito primario di Hello dispone di un cluster contenente cinque server Hyper-V con 470 macchine virtuali.
* macchine virtuali Hello eseguire diversi carichi di lavoro e tutte è abilitata la protezione Azure Site Recovery.
* Spazio di archiviazione per nodo cluster hello viene fornito da una rete SAN iSCSI. Modello – Hitachi HUS130.
* Ogni server del cluster ha quattro schede di rete (NIC) di 1 Gbps ciascuna.
* Sono due delle schede di rete hello rete privata iSCSI tooan connesso e due rete aziendale esterna tooan connesso. Una delle reti esterne hello è riservata solo le comunicazioni del cluster.

![Requisiti hardware principali](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Server | RAM | Modello | Processore | Numero di processori | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Server Hyper-V nel cluster:  <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25 ha 256 |Dell ™ PowerEdge ™ R820 |CPU Intel(R) Xeon(R) E5-4620 0 @ 2,20 GHz |4 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + ruolo Hyper-V  |
| Server VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>Sito secondario (ripristino)

* sito secondario Hello dispone di un cluster di failover con sei nodi.
* Spazio di archiviazione per nodo cluster hello viene fornito da una rete SAN iSCSI. Modello – Hitachi HUS130.

![Specifiche hardware principali](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Server | RAM | Modello | Processore | Numero di processori | NIC | Software |
| --- | --- | --- | --- | --- | --- | --- |
| Server Hyper-V nel cluster:  <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |CPU Intel(R) Xeon(R) E5-2630 0 @ 2,30 GHz |2 |I Gbps x 4 |Windows Server Datacenter 2012 R2 (x64) + ruolo Hyper-V  |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |CPU Intel(R) Xeon(R) E5-4620 0 @ 2,20 GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + ruolo Hyper-V  |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |CPU Intel(R) Xeon(R) E5-4620 0 @ 2,20 GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + ruolo Hyper-V  |
| Server VMM |2 | | |2 |1 Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Carichi di lavoro server

* A scopo di test sono stati scelti i carichi di lavoro comunemente utilizzati negli scenari aziendali dei clienti.
* Utilizziamo [IOMeter](http://www.iometer.org) con caratteristiche del carico di lavoro hello riepilogati nella tabella hello per la simulazione.
* Tutti i profili IOMeter sono impostati i modelli di toowrite byte casuali toosimulate scrittura peggiori per carichi di lavoro.

| Carico di lavoro | Dimensioni I/O (KB) | % accesso | % lettura | I/O in sospeso | Modello I/O |
| --- | --- | --- | --- | --- | --- |
| File Server |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |Tutti 100% casuale |
| SQL Server (volume 1) SQL Server (volume 2) |864 |100%100% |70%0% |88 |100% casuale 100% sequenziale |
| Exchange |32 |100% |67% |8 |100% casuale |
| Workstation/VDI |464 |66%34% |70%95% |11 |Entrambi 100% casuale |
| File Server Web |4864 |33%34%33% |95%95%95% |888 |Tutti 75% casuale |

### <a name="vm-configuration"></a>Configurazione della macchina virtuale

* 470 macchine virtuali nel cluster primario hello.
* Tutte le macchine virtuali con disco VHDX.
* Macchine virtuali in esecuzione di carichi di lavoro riepilogati nella tabella hello. Tutti sono stati creati con i modelli VMM.

| Carico di lavoro | N. di macchine virtuali | RAM minima (GB) | RAM massima (GB) | Dimensioni disco logico (GB) per macchina virtuale | Numero massimo di IOPS |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| File Server |50 |1 |2 |552 |22 |
| VDI |149 |0,5 |1 |80 |6 |
| Server Web |149 |0,5 |1 |80 |6 |
| TOTALE |470 | | |96,83 TB |4108 |

### <a name="site-recovery-settings"></a>Impostazioni di Site Recovery

* Azure Site Recovery è stato configurato per la protezione di tooon tra più sedi locali
* server VMM Hello ha quattro cloud configurati contenenti i server di cluster Hyper-V hello e le macchine virtuali.

| Cloud VMM primario | Macchine virtuali protette nei cloud hello | Frequenza di replica | Punti di ripristino aggiuntivi |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 min |Nessuno |
| PrimaryCloudRpo30s |47 |30 secondi |Nessuno |
| PrimaryCloudRpo30sArp1 |47 |30 secondi |1 |
| PrimaryCloudRpo5m |235 |5 min |Nessuno |

### <a name="performance-metrics"></a>Metriche delle prestazioni

tabella di Hello sono riepilogate le metriche delle prestazioni di hello e i contatori misurati nella distribuzione hello.

| Metrica | Contatore |
| --- | --- |
| CPU |\Processor(_Total)\% Processor Time |
| Memoria disponibile |\Memoria\MByte disponibili |
| IOPS |\DiscoFisico(_Totale)\Trasferimenti disco/secondo |
| Operazioni di lettura VM (IOPS) al secondo  |\Dispositivo di archiviazione Hyper-V (<VHD>)\Operazioni di lettura/secondo |
| Operazioni di scrittura VM (IOPS) al secondo |\Dispositivo di archiviazione virtuale Hyper-V (<VHD>)\Operazioni di scrittura/S |
| Velocità effettiva lettura VM |\Dispositivo di archiviazione virtuale Hyper-V (<VHD>)\Byte letti al secondo |
| Velocità effettiva di scrittura VM |\Dispositivo di archiviazione virtuale Hyper-V(<VHD>)\Byte scritti al secondo |

## <a name="next-steps"></a>Passaggi successivi

[Configurare la replica tra due siti VMM locali](site-recovery-vmm-to-vmm.md)
