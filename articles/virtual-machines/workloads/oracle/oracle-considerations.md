---
title: soluzioni aaaOracle in Microsoft Azure | Documenti Microsoft
description: Informazioni sulle configurazioni supportate e sulle limitazioni delle soluzioni Oracle in Microsoft Azure.
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Soluzioni Oracle e rispettiva distribuzione in Microsoft Azure
Questo articolo vengono illustrate le informazioni necessarie toosuccesfully distribuire diverse soluzioni di Oracle in Microsoft Azure. Queste soluzioni sono basate su immagini di macchina virtuale pubblicate da Oracle hello Azure Marketplace. tooget un elenco di immagini disponibili, eseguire hello comando seguente:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
A partire da elenco hello 6-16-2017 delle immagini sono i seguenti hello:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Queste immagini sono considerate di tipo "Bring Your Own License" e verranno quindi addebitati solo i costi di calcolo, archiviazione e rete sostenuti durante l'esecuzione di una VM.  Si presuppone essere toouse correttamente concesso in licenza il software Oracle e si dispone di un contratto di assistenza sul posto con Oracle. Oracle garantisce mobilità delle licenze da tooAzure locale. Vedere hello pubblicato [Oracle e Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Nota Per informazioni dettagliate sulla mobilità delle licenze. 

Utenti singoli possono anche scegliere toobase le relative soluzioni in immagini personalizzate vengono creare da zero in Azure oppure caricare un'immagine personalizzata da ambienti locale su.

## <a name="support-for-jd-edwards"></a>Supporto per JD Edwards
In base nota supporto tooOracle [2178595.1 ID documento](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne versioni 9.2 e versioni successive sono supportate in **qualsiasi public cloud offerta** che soddisfa le specifiche `Minimum Technical Requirements` (MTR).  Sarà necessario immagini personalizzate toocreate che soddisfano le specifiche di MTR per la compatibilità delle applicazioni del sistema operativo e software. 

## <a name="oracle-database-virtual-machine-images"></a>Immagini di macchine virtuali Oracle Database
Oracle supporta l'esecuzione di Oracle DB 12.1 Standard ed Enterprise Edition in Azure nelle immagini di macchine virtuali basate su Oracle Linux.  Immagine di macchina virtuale hello tooproperly dimensioni assicurarsi di essere hello migliori prestazioni per i carichi di lavoro del database Oracle in Azure e usare dischi gestiti che sono supportate da archiviazione Premium. Per istruzioni su come tooquickly ottenere un database Oracle in esecuzione in Azure utilizzando hello Oracle pubblicata immagine di macchina virtuale, [provare questa procedura dettagliata delle Guide rapide di Oracle DB hello](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Opzioni di configurazione dei dischi collegati

I dischi collegati si basano su hello servizio di archiviazione Blob di Azure. Ogni disco standard è in grado di supportare un massimo teorico di circa 500 operazioni di input/output al secondo (IOPS). Offerta premium disco preferito per i carichi di lavoro database ad alte prestazioni e ottenere backup too5000 di IOps per disco. Sebbene sia possibile utilizzare un singolo disco se che soddisfa le prestazioni è necessario: è possibile migliorare prestazioni IOPS effettive hello se utilizzare più dischi collegati, distribuire i dati del database su di essi e quindi utilizzare Oracle Automatic Storage Management (ASM). Per altre informazioni specifiche per Oracle ASM, vedere [Oracle Automatic Storage overview](http://www.oracle.com/technetwork/database/index-100339.html) (Panoramica di Oracle Automatic Storage). Per un esempio di come tooinstall e configurare Oracle ASM in una VM Linux di Azure: è possibile provare hello [installazione e configurazione di gestione di archiviazione automatica di Oracle](configure-oracle-asm.md) esercitazione.

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle Realtime Application Cluster (RAC)
Oracle RAC è progettato toomitigate hello errore di un singolo nodo in una configurazione di multi-node cluster locale.  Si basa su due tecnologie locale che non sono gli ambienti di cloud pubblico toohyper a livello nativo: multi-cast di rete e disco condiviso. Sono disponibili soluzioni di terze parti create da aziende [, ad esempio FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) che emulare queste tecnologie, se è necessario toodeploy Oracle RAC in Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Considerazioni sulla disponibilità elevata e sul ripristino di emergenza
Quando si utilizzano database Oracle in Azure, è responsabile per l'implementazione di un'elevata disponibilità e ripristino soluzione tooavoid alcun tempo di inattività. 

La disponibilità elevata e il ripristino di emergenza per Oracle Database Enterprise Edition (senza RAC) su Azure possono essere ottenuti usando [Data Guard, Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) oppure [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), con due database in due macchine virtuali separate. Entrambe le macchine virtuali devono essere in hello stesso [rete virtuale](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure che possano accedere reciprocamente sull'indirizzo IP permanente privato di hello.  È inoltre consigliabile hello le macchine virtuali in hello stesso set di disponibilità di Azure tooplace tooallow in separato domini di errore e domini di aggiornamento.  Se si vuole toohave con ridondanza geografica, è possibile avere questi due database vengono replicati tra due aree diverse e connettersi due istanze di hello con un Gateway VPN.

È disponibile un'esercitazione "[implementare Oracle DataGuard in Azure](configure-oracle-dataguard.md)" che illustra tootrial procedura di installazione di base hello ciò in Azure.  

Con Oracle Data Guard, la disponibilità elevata può essere ottenuta con un database primario in una macchina virtuale, un database secondario (standby) in un'altra macchina virtuale e la replica unidirezionale configurata tra di essi. il risultato di Hello è l'accesso in lettura toohello copia del database hello. Oracle goldengate, è possibile configurare la replica bidirezionale tra due database hello. toolearn tooset di una soluzione a disponibilità elevata per i database mediante questi strumenti, vedere [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) e [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentazione nel sito Web Oracle hello. Se è necessario lettura / scrittura accesso toohello copia del database di hello, è possibile utilizzare [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

È disponibile un'esercitazione "[implementare Oracle GoldenGate in Azure](configure-oracle-golden-gate.md)" che illustra hello seup base procedura tootrial ciò in Azure.

Nonostante entrambe abbiano una soluzione a disponibilità elevata e ripristino di emergenza progettata in Azure, è opportuno tooensure si dispone di una strategia di backup in toorestore sul posto del database.  È disponibile un'esercitazione [Backup e ripristinare un Database Oracle](oracle-backup-recovery.md) che illustra procedura di base per la creazione di un backup consistant hello.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Immagini di macchine virtuali Oracle WebLogic Server
* **Il clustering è supportato solo nella Enterprise Edition.** Il licenziatario potrà toouse clustering WebLogic solo quando si utilizza hello WebLogic Server Enterprise Edition. Non utilizzare il clustering con WebLogic Server Standard Edition.
* **Il multicast UDP non è supportato.** Azure supporta l'unicast UDP, ma non il multicast e il broadcast. WebLogic Server è in grado di toorely nella capacità di unicast UDP di Azure. Per i migliori risultati unicast UDP, si consiglia di dimensioni del cluster WebLogic hello rimanere statico, o rimanere con non più di 10 server gestiti inclusi nel cluster hello.
* **WebLogic Server si aspetta hello toobe porte pubbliche e private uguale per T3 accedere (ad esempio, quando si usa Enterprise JavaBeans).** Prendere in considerazione uno scenario a più livelli in cui un'applicazione di livello di servizio (EJB) è in esecuzione su un cluster WebLogic Server costituito da due o più VM in una rete virtuale denominata **SLWLS**. livello di client hello è in una subnet diversa in hello stessa rete virtuale, un semplice programma Java toocall EJB nel livello di servizio hello durante il tentativo di esecuzione. Poiché si tratta di livello di servizio hello saldo tooload necessarie, un endpoint con bilanciamento del carico pubblico deve toobe creato per hello macchine virtuali in cluster WebLogic Server hello. Se la porta privata hello specificati è diversa dalla porta pubblica hello (ad esempio, 7006:7008), si verifica un errore come illustrato di seguito hello:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Infatti, per qualsiasi accesso remoto T3 WebLogic Server prevede che la porta del servizio di bilanciamento carico di hello e hello gestito WebLogic server porta toobe hello stesso. In hello prima di case, hello client accede alla porta 7006 (porta di bilanciamento carico di hello) e server gestito hello è in ascolto sulla porta 7008 (porta privata hello). Questa restrizione è applicabile solo per l'accesso T3 e non per quello HTTP.

   tooavoid questo problema, utilizzare uno dei seguenti soluzioni alternative hello:

  * Utilizzare hello stesso privata e i numeri di porta pubblica per il carico bilanciato accesso tooT3 endpoint dedicato.
  * Includere hello segue il parametro di JVM, quando si avvia WebLogic Server:

         -Dweblogic.rjvm.enableprotocolswitch=true

Per informazioni correlate, vedere l'articolo KB **860340.1** all’indirizzo <http://support.oracle.com>.

* **Limitazioni del clustering dinamico e del bilanciamento del carico.** Si supponga che si desidera toouse un cluster dinamico in WebLogic Server ed esporlo tramite un singolo, pubblico con bilanciamento del carico endpoint in Azure. A tale scopo, purché si utilizzi un numero di porta fissa per ognuno dei hello server (non in modo dinamico assegnato da un intervallo) gestiti e non avvia più server gestiti superiore a quello di amministratore di hello tiene traccia delle macchine (vale a dire non più di un server gestito per ogni virt registrazione accesso utenti macchina). Se la configurazione comporta più WebLogic Server in corso l'avvio di macchine virtuali (ovvero, in cui più condivisione di istanze di WebLogic Server hello stessa macchina virtuale), quindi non è possibile che più di uno di tali istanze di WebLogic Server tooa toobind di server specificato numero di porta: hello ad altri utenti che la macchina virtuale avrà esito negativo.

   In hello altra parte, se si configura hello Amministrazione server tooautomatically assegnare numeri di porta univoci tooits gestiti server, il bilanciamento del carico non è possibile poiché Azure non supporta il mapping da una singola porta pubblica toomultiple privata porte come sarebbe obbligatorio per questa configurazione.
* **Più istanze di WebLogic in una macchina virtuale.** A seconda dei requisiti della distribuzione, si potrebbe prendere in considerazione hello opzione dell'esecuzione di più istanze di WebLogic Server su hello stessa macchina virtuale, se la macchina virtuale di hello è sufficientemente grande. Ad esempio, in una macchina virtuale di medie dimensioni, che contiene due core, è possibile scegliere toorun due istanze di WebLogic Server. Si noti tuttavia che è comunque consigliabile evitare di introdurre singoli punti di errore nell'architettura, che dovrebbe essere case hello se è stata utilizzata una sola macchina virtuale che esegue più istanze di WebLogic Server. L’utilizzo di almeno due macchine virtuali potrebbe rappresentare un approccio migliore e ciascuna delle macchine virtuali potrebbe eseguire più istanze di WebLogic Server. Ognuna di queste istanze di WebLogic Server può essere ancora parte di hello dello stesso cluster. Si noti, tuttavia, non è attualmente possibile toouse bilanciamento tooload Azure endpoint esposti da tali distribuzioni di WebLogic Server all'interno di hello stessa macchina virtuale, perché servizio di bilanciamento del carico di Azure richiede hello server con carico bilanciato toobe distribuiti macchine virtuali univoche.

## <a name="oracle-jdk-virtual-machine-images"></a>Immagini di macchine virtuali Oracle JDK
* **Aggiornamenti più recenti di JDK 6 e 7.** Mentre si consiglia di utilizzare hello pubblica più recente supportato versione di Java (attualmente Java 8), Azure rende JDK 6 e 7 immagini disponibili. Si tratta per le applicazioni legacy che non sono ancora pronti toobe aggiornato tooJDK 8. Mentre gli aggiornamenti tooprevious JDK immagini potrebbero non essere più disponibile toohello pubblico, dato hello Microsoft collaborano con Oracle, hello JDK 6 e 7 immagini fornite da Azure sono destinate toocontain un aggiornamento più recente di pubblici normalmente offerta da I clienti supportati Oracle tooonly a un gruppo selezionato di Oracle. Le nuove versioni delle immagini JDK hello verranno resa disponibile nel corso del tempo con versioni aggiornate di JDK 6 e 7.

   Hello JDK disponibile in questa JDK 6 e 7 immagini e le macchine virtuali hello e derivate da tali immagini sono utilizzabili solo all'interno di Azure.
* **JDK a 64 bit.** immagini di macchina virtuale Oracle WebLogic Server Hello e immagini di macchine virtuali Oracle JDK hello fornite da Azure contengono versioni a 64 bit di Windows Server e JDK hello hello.

## <a name="next-steps"></a>Passaggi successivi
È ora disponibile una panoramica delle soluzioni Oracle correnti in Microsoft Azure. Il passaggio successivo è toogo e distribuire il primo Database Oracle in Azure.
- Provare a hello [crea un Database Oracle in Azure](oracle-database-quick-create.md) tooget esercitazione introduttiva.
