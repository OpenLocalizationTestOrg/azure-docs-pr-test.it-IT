---
title: aaaDesign e implementare Oracle database in Azure | Documenti Microsoft
description: Progettare e implementare un database Oracle nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Progettare e implementare un database Oracle in Azure

## <a name="assumptions"></a>Presupposti

- Si sta pianificando toomigrate un database Oracle da tooAzure locale.
- È necessario comprendere di hello diverse metriche in Oracle il report.
- Si ha una conoscenza di base delle prestazioni delle applicazioni e dell'utilizzo della piattaforma.

## <a name="goals"></a>Obiettivi

- Comprendere come toooptimize la distribuzione di Oracle in Azure.
- Esplorare le opzioni di ottimizzazione delle prestazioni per un database Oracle in un ambiente Azure.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>differenze tra una locale Hello e implementazione di Azure 

Di seguito sono alcune importanti tookeep operazioni utili quando esegue la migrazione di applicazioni tooAzure in locale. 

Una differenza importante è che in un'implementazione in Azure le risorse, ad esempio VM, dischi e reti virtuali, vengono condivise con gli altri client. Inoltre, le risorse possono essere limitate in base ai requisiti di hello. Invece di porre l'attenzione per evitare errori (MTBF), Azure più è incentrata sulla sopravvivenza errore hello (MTTR).

Hello nella tabella seguente sono elencate alcune delle differenze di hello tra un'implementazione locale e un'implementazione di un database Oracle.

> 
> |  | **Implementazione locale** | **Implementazione in Azure** |
> | --- | --- | --- |
> | **Rete** |LAN/WAN  |SDN (Software Defined Networking)|
> | **Gruppo di sicurezza** |Strumenti di restrizione per indirizzi IP/porte |[Gruppo di sicurezza di rete (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Resilienza** |MTBF (tempo medio tra gli errori) |MTTR (tempo medio toorecovery)|
> | **Manutenzione pianificata** |Applicazione di patch/aggiornamenti|[Set di disponibilità](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (applicazione di patch/aggiornamenti gestita da Azure) |
> | **Risorsa** |Dedicato  |Condivisa con altri client|
> | **Aree** |Data center |[Coppie di aree](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Archiviazione** |Dischi fisici/SAN |[Archiviazione gestita da Azure](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Ridimensionare** |Scalabilità verticale |Scalabilità orizzontale|


### <a name="requirements"></a>Requisiti

- Determinare tasso di crescita e di dimensioni di database hello.
- Determinare i requisiti di IOPS hello, che è possibile stimare basato su Oracle il report o altri strumenti di monitoraggio di rete.

## <a name="configuration-options"></a>Opzioni di configurazione

Esistono quattro possibili aree che è possibile ottimizzare le prestazioni di tooimprove in un ambiente Azure:

- Dimensioni della macchina virtuale
- Velocità effettiva della rete
- Tipi di disco e configurazioni
- Impostazioni della cache su disco

### <a name="generate-an-awr-report"></a>Generare un report AWR

Se si dispone di un database Oracle e si intende toomigrate tooAzure, sono disponibili diverse opzioni. È possibile eseguire hello Oracle il report tooget hello metriche (IOPS Mbps, GiBs e così via). Scegliere quindi hello che macchina virtuale in base alle metriche di hello raccolti. Oppure è possibile contattare le informazioni di infrastruttura team tooget simile.

È possibile valutare se eseguire il report AWR durante i carichi di lavoro sia normali che di picco, per poter effettuare un confronto. In base a questi report, è possibile ridimensionare le macchine virtuali in base a carico di lavoro medio hello o carico di lavoro massimo hello hello.

Ecco un esempio di come un report AWR toogenerate:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Metriche principali

Di seguito sono metriche hello che è possibile ottenere dal report AWR hello:

- Numero totale di core
- Velocità di clock della CPU
- Memoria totale in GB
- Uso della CPU
- Velocità di trasferimento dati di picco
- Frequenza delle modifiche di I/O (lettura/scrittura)
- Velocità del log di ripristino (Mbps)
- Velocità effettiva della rete
- Latenza di rete (bassa/alta)
- Dimensioni del database in GB
- Byte ricevuti tramite SQL * Net da / tooclient

### <a name="virtual-machine-size"></a>Dimensioni della macchina virtuale

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Stima delle dimensioni della macchina virtuale in base all'utilizzo della CPU, memoria e i/o da hello report AWR

È possibile esaminare è hello primi cinque programmato in primo piano eventi che indicano dove hello i colli di bottiglia.

Ad esempio, nel seguente diagramma di hello, sincronizzazione file di log hello è nella parte superiore di hello. Indica il numero di hello di attese di che sono necessari prima di hello LGWR scrive il file di log rollforward hello log buffer toohello. Questi risultati indicano che è necessario migliorare le prestazioni della risorsa di archiviazione o dei dischi. Inoltre, hello diagramma mostra anche la hello numero di CPU (Core) e la quantità di hello di memoria.

![Schermata di hello AWR della pagina di report](./media/oracle-design/cpu_memory_info.png)

Hello diagramma seguente mostra i/o totale di hello di lettura e scrittura. Si sono verificati 59 leggere e 247.3 GB scritti durante la fase di hello del report hello.

![Schermata di hello AWR della pagina di report](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Scegliere una VM

In base alle informazioni di hello raccolti da hello report AWR, hello è toochoose una macchina virtuale di dimensioni simili che soddisfi i requisiti. È possibile trovare un elenco delle macchine virtuali disponibili nell'articolo hello [ottimizzazione per la memoria](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Ottimizzare il ridimensionamento di VM hello con una serie di macchine Virtuali simile in base a hello ACU

Dopo aver scelto hello VM, prestare attenzione toohello ACU per hello macchina virtuale. È possibile scegliere una diversa macchina virtuale in base a hello valore ACU più adatto alle proprie esigenze. Per altre informazioni, vedere [Unità di calcolo di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Schermata della pagina di hello ACU unità](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Velocità effettiva della rete

Hello seguente diagramma mostra la relazione hello tra velocità effettiva e IOPS:

![Screenshot della velocità effettiva](./media/oracle-design/throughput.png)

velocità effettiva di rete totale Hello viene stimata in base a hello le seguenti informazioni:
- Traffico SQL*Net
- Mbps x numero di server (flusso in uscita, ad esempio Oracle Data Guard)
- Altri fattori, ad esempio la replica dell'applicazione

![Schermata di hello SQL * Net velocità effettiva](./media/oracle-design/sqlnet_info.png)

In base ai requisiti di larghezza di banda di rete, esistono diversi tipi di gateway per toochoose da. ad esempio Basic, VpnGw e Azure ExpressRoute. Per ulteriori informazioni, vedere hello [gateway VPN di pagina dei prezzi](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Raccomandazioni**

- Latenza di rete è maggiore rispetto tooan locale la distribuzione. La riduzione dei round trip di rete può migliorare notevolmente le prestazioni.
- round trip tooreduce, consolidare le applicazioni che presentano le transazioni di elevata o di applicazioni "chatty" hello stessa macchina virtuale.

### <a name="disk-types-and-configurations"></a>Tipi di disco e configurazioni

- *Dischi del sistema operativo predefiniti*: questi tipi di dischi offrono dati persistenti e memorizzazione nella cache. Sono ottimizzati per l'accesso del sistema operativo all'avvio e non sono progettati per i carichi di lavoro transazionali o di data warehouse (analitici).

- *Non gestita dischi*: con questi tipi di disco, gestire gli account di archiviazione hello che archiviano i file di disco rigido virtuale (VHD) hello corrispondenti tooyour dischi di macchina virtuale. I file VHD vengono archiviati come BLOB di pagine in account di archiviazione di Azure.

- *Dischi gestiti*: Azure gestisce gli account di archiviazione hello utilizzati per i dischi di macchina virtuale. Specificare tipo di disco hello (standard o premium) e dimensioni di hello del disco hello che è necessario. Azure crea e gestisce disco hello per l'utente.

- *Dischi di archiviazione Premium*: questi tipi di dischi sono ideali per i carichi di lavoro di produzione. I dischi Premium archiviazione supporta VM che possono essere collegati serie toospecific dimensioni macchine virtuali, ad esempio le macchine virtuali di serie DS, DSv2, GS e F. disco premium Hello viene fornito con diverse dimensioni e, è possibile scegliere tra dischi compreso tra 32 GB too4, 096 GB. Ciascuna dimensione di disco ha le proprie specifiche in termini di prestazioni. A seconda dei requisiti dell'applicazione, è possibile collegare uno o più dischi tooyour macchina virtuale.

Quando si crea un nuovo disco gestito dal portale di hello, è possibile scegliere hello **tipo di Account** per il tipo di hello del disco si desidera toouse. Tenere presente che non tutti i dischi disponibili vengono visualizzati nel menu a discesa hello. Dopo aver scelto una determinata dimensione di macchina virtuale, menu hello Mostra solo hello disponibili archiviazione premium gli SKU di cui si basano sulle dimensioni di macchina virtuale.

![Schermata della pagina di hello disco gestito](./media/oracle-design/premium_disk01.png)

Per altre informazioni, vedere [Archiviazione Premium a prestazioni elevate e dischi gestiti per le VM](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Dopo aver configurato lo spazio di archiviazione in una macchina virtuale, è possibile dischi di hello tooload test prima di creare un database. La conoscenza di velocità dei / o hello in termini di latenza e velocità effettiva possono aiutare a determinare se le macchine virtuali hello supportano hello previsto velocità effettiva con destinazioni di latenza.

Sono disponibili numerosi strumenti per il test di carico delle applicazioni, ad esempio Oracle Orion, Sysbench e Fio.

Dopo aver distribuito un database Oracle, eseguire nuovamente il test di carico hello. Avviare i carichi di lavoro di picco e regolare e hello Mostra risultati si hello linea di base dell'ambiente.

Potrebbe essere più importante dell'archiviazione di hello toosize basata sulla frequenza di IOPS hello anziché dimensioni di archiviazione hello. Ad esempio, se hello necessario IOPS è pari a 5000, ma è necessario solo 200 GB, si potrebbe comunque ottenere hello P30 classe premium disco a anche se è dotato di più di 200 GB di spazio di archiviazione.

frequenza delle operazioni IOPS Hello può essere ottenuto dalla hello report AWR. Infatti è determinato dalla frequenza di scritture log di ripristino hello e letture fisiche.

![Schermata di hello AWR della pagina di report](./media/oracle-design/awr_report.png)

Ad esempio, dimensioni di rollforward hello sono 12,200,000 byte al secondo, ovvero too11.63 uguale MBPs.
Hello IOPS è 12.200.000 / 2,358 = 5,174.

Dopo avere un quadro preciso dei requisiti dei / o hello, è possibile scegliere una combinazione di unità che sono più adatti toomeet tali requisiti.

**Raccomandazioni**

- Per spazio di tabella di dati, suddividere i del carico di lavoro di hello i/o su un numero di dischi, utilizzando Oracle ASM o l'archiviazione gestita.
- Man mano che aumenta di dimensione del blocco dei / o hello per le operazioni di lettura a utilizzo intensivo ed elevato della scrittura, è possibile aggiungere altri dischi dati.
- Aumentare la dimensione del blocco hello per processi sequenziali di grandi dimensioni.
- Utilizzare i/o tooreduce di compressione dei dati (per i dati e indici).
- Separare i log di rollforward, di sistema e temporanei e annullare TS nei dischi dati separati.
- Non inserire alcun file dell'applicazione nei dischi del sistema operativo predefiniti (dev/sda). Questi dischi non sono ottimizzati per l'avvio rapido delle macchine virtuali e potrebbero non offrire prestazioni valide per l'applicazione.

### <a name="disk-cache-settings"></a>Impostazioni della cache su disco

Sono disponibili tre opzioni per la memorizzazione nella cache dell'host:

- *Sola lettura*: tutte le richieste sono memorizzate nella cache per le letture future. Tutte le scritture rese persistenti direttamente tooAzure nell'archiviazione Blob.

- *Lettura/scrittura*: si tratta di un algoritmo "read-ahead". Hello letture e scritture vengono memorizzati nella cache per le letture future. Operazioni di scrittura non write-through sono persistenti prima la cache locale toohello. Per SQL Server, operazioni di scrittura sono persistenti tooAzure archiviazione perché utilizza write-through. Fornisce inoltre una latenza del disco più bassa hello per carichi di lavoro leggeri.

- *Nessuna* (disabilitato): tramite questa opzione, è possibile ignorare la cache di hello. Tutti i dati di hello toodisk trasferiti viene conservato tooAzure archiviazione. In questo modo di metodo hello massima velocità dei / o per carichi di lavoro con utilizzo intensivo dei / o. È inoltre necessario tootake "costo della transazione" in considerazione.

**Raccomandazioni**

velocità effettiva di hello toomaximize, è consigliabile iniziare con **Nessuno** per la memorizzazione nella cache dell'host. Archiviazione Premium, tenere presente che è necessario disattivare barriere"hello" quando si monta hello file system con hello **ReadOnly** o **Nessuno** opzioni. Aggiornare file /etc/fstab. hello con dischi toohello UUID di hello.

Per altre informazioni, vedere [Archiviazione Premium per VM Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Schermata della pagina di hello disco gestito](./media/oracle-design/premium_disk02.png)

- Per i dischi del sistema operativo, usare la memorizzazione nella cache **Lettura/scrittura** predefinita.
- Per SYSTEM, TEMP e UNDO usare **Nessuna** per la memorizzazione nella cache.
- Per DATA usare **Nessuna** per la memorizzazione nella cache, ma se il database è di sola lettura o esegue un'intensa attività di lettura, usare la memorizzazione nella cache **Sola lettura**.

Dopo aver salvato l'impostazione del disco dati, è possibile modificare l'impostazione della cache di hello host a meno che non si unità hello hello livello del sistema operativo, smontare e rimontare quindi dopo aver apportato hello modificare.


## <a name="security"></a>Sicurezza

Dopo aver impostato e configurato l'ambiente di Azure, hello è toosecure della rete. Di seguito sono elencati alcuni suggerimenti:

- *Criteri del gruppo di sicurezza di rete*: il gruppo di sicurezza di rete può essere definito da una subnet o una scheda di interfaccia di rete. È più semplice toocontrol accesso a livello di subnet hello sia per la sicurezza e forza il routing per elementi come i firewall di applicazione.

- *Jumpbox*: per l'accesso più sicuro, gli amministratori devono non connettere direttamente toohello applicazione servizio o il database. Un jumpbox viene utilizzato come una media tra il computer di amministrazione di hello e risorse di Azure.
![Schermata della pagina di topologia Jumpbox hello](./media/oracle-design/jumpbox.png)

    computer amministratore Hello deve offrire l'accesso con restrizioni IP toohello jumpbox solo. Hello jumpbox deve avere accesso toohello applicazione e database.

- *Rete privata* (subnet): si consiglia di disporre del database e del servizio dell'applicazione hello in subnet separate, pertanto un migliore controllo può essere impostato dai criteri di gruppo.


## <a name="additional-reading"></a>Informazioni aggiuntive

- [Configurare Oracle ASM](configure-oracle-asm.md)
- [Configurare Oracle Data Guard](configure-oracle-dataguard.md)
- [Configurare Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Backup e ripristino di Oracle](oracle-backup-recovery.md)

## <a name="next-steps"></a>Passaggi successivi

- [Esercitazione: Creare VM a disponibilità elevata](../../linux/create-cli-complete.md)
- [Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM](../../linux/cli-samples.md)
