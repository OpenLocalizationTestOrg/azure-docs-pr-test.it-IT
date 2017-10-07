---
title: il mapping di rete per la replica di macchina virtuale Hyper-V con il ripristino del sito aaaPlan | Documenti Microsoft
description: Configurare il mapping di rete per la replica della macchina virtuale Hyper-V da un tooAzure Data Center locale o un sito secondario tooa.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Pianificare il mapping di rete per la replica di macchine virtuali Hyper-V con Site Recovery



In questo articolo consente di piano per la rete mapping durante la replica delle macchine virtuali Hyper-V tooAzure o tooa di sito secondario, utilizzando hello e toounderstand [servizio Azure Site Recovery](site-recovery-overview.md).

Dopo aver letto questo articolo inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Mapping di rete per la replica tooAzure

Mapping di rete viene utilizzato la replica tooAzure macchine virtuali Hyper-V (gestito in VMM). Il mapping di rete esegue il mapping tra reti VM in un server VMM e reti di Azure di destinazione. Mapping hello seguenti:

- **Connessione di rete**: assicura che replicate le macchine virtuali di Azure connessa toohello di rete mappate. Tutti i computer in cui eseguire il failover su hello stessa rete possa connettersi tooeach altri, anche se è stato eseguito il failover nei piani di ripristino diverso.
- **Gateway di rete**, ovvero se nella rete Azure di destinazione hello è stato configurato un gateway di rete, le macchine virtuali possono connettersi le macchine virtuali tooother locale.

Si noti che:

- Si esegue il mapping un'origine tooan rete VM di VMM rete virtuale di Azure.
- Dopo il failover le macchine virtuali di Azure in hello rete di origine verrà connesso toohello rete virtuale di destinazione mappata.
- Aggiunta di nuove macchine virtuali toohello rete VM di origine connessi toohello eseguito il mapping di rete di Azure, quando viene eseguita la replica.
- Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica si connette toothat subnet di destinazione dopo il failover.
- Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello si connette toohello prima subnet nella rete hello.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Mapping di rete per Data Center secondario tooa di replica

Mapping di rete viene utilizzato la replica Data Center secondario tooa di macchine virtuali Hyper-V (gestito in System Center Virtual Machine Manager (VMM)). Il mapping di rete esegue il mapping tra reti VM in un server VMM di origine e reti VM in un server VMM di destinazione. Mapping hello seguenti:

- **Connessione di rete**, ovvero le reti di macchine virtuali si connette tooappropriate dopo il failover. replica di Hello VM verrà connesso toohello rete di destinazione di rete di origine mappata toohello.
- **Durante il posizionamento**, in modo ottimale decimali hello macchine virtuali di replica nel server host Hyper-V. Macchine virtuali di replica vengono posizionate in host che possono hello accesso alle reti VM mappate.
- **Nessun mapping di rete**, se non si configura il mapping di rete, le macchine virtuali di replica non sarà le reti VM tooany connesse dopo il failover.

Si noti che:

- Mapping di rete può essere configurato tra reti VM nei due server VMM o in un singolo server VMM se due siti sono gestiti da hello stesso server.
- Quando il mapping è configurato correttamente e la replica è abilitata, una macchina virtuale nella posizione primaria hello sarà connessa tooa rete e la replica nel percorso di destinazione hello verrà connessa tooits eseguito il mapping di rete.
-
- Se le reti impostate correttamente in VMM, quando si seleziona una rete VM di destinazione durante il mapping di rete, cloud di origine VMM hello che utilizzano una rete VM di origine hello verrà visualizzato, insieme a reti VM di destinazione disponibili hello nei cloud di destinazione hello che vengono utilizzati per protezione dati.
- Se la rete di destinazione hello dispone di più subnet e una di queste subnet ha hello stesso nome come hello subnet in cui hello macchina virtuale di origine si trova quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.



### <a name="example"></a>Esempio

Ecco un esempio tooillustrate questo meccanismo. Si prenda come esempio un’organizzazione con due sedi, New York e Chicago.

**Posizione** | **Server VMM** | **Reti VM** | **Mappata a**
---|---|---|---
New York | VMM-NewYork| VMNetwork1-NewYork | Mappato tooVMNetwork1-Chicago
 |  | VMNetwork2-NewYork | Non mappata
Chicago | VMM-Chicago| VMNetwork1-Chicago | TooVMNetwork1-NewYork mappato
 | | VMNetwork1-Chicago | Non mappata

Esempio:

- Creazione di una macchina virtuale di replica per ogni macchina virtuale che è connesso tooVMNetwork1-NewYork, verrà connesso tooVMNetwork1-Chicago.
- Quando una macchina virtuale di replica viene creata per VMNetwork2-NewYork o VMNetwork2-Chicago, non sarà connessa tooany rete.

Ecco come vengono impostati cloud VMM, organizzazione di esempio e le reti logiche di hello associate hello cloud.

#### <a name="cloud-protection-settings"></a>Impostazioni di protezione del cloud

**Cloud protetto** | **Protezione del cloud** | **Rete logica (New York)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>
SilverCloud2 | <p>ND</p><p></p> | <p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Impostazioni di rete VM e logica

**Posizione** | **Rete logica** | **Rete VM associata**
---|---|---
New York | LogicalNetwork1-NewYork | VMNetwork1-NewYork
Chicago | LogicalNetwork1-Chicago | VMNetwork1-Chicago
 | LogicalNetwork2Chicago | VMNetwork2-Chicago

#### <a name="target-network-settings"></a>Impostazioni di rete di destinazione

In base a queste impostazioni, quando si seleziona una rete VM di destinazione hello, hello nella tabella seguente mostra le scelte di hello che saranno disponibili.

**Select** | **Cloud protetto** | **Protezione del cloud** | **Rete di destinazione disponibili**
---|---|---|---
VMNetwork1-Chicago | SilverCloud1 | SilverCloud2 | Disponibile
 | GoldCloud1 | GoldCloud2 | Disponibile
VMNetwork2-Chicago | SilverCloud1 | SilverCloud2 | Non disponibile
 | GoldCloud1 | GoldCloud2 | Disponibile


Se la rete di destinazione hello dispone di più subnet e una di queste subnet ha hello stesso nome come hello subnet in cui hello macchina virtuale di origine si trova quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.


#### <a name="failback-behavior"></a>Comportamento di failback

toosee cosa accade nel caso di hello di failback (replica inversa), si supponga che VMNetwork1-NewYork è mappato tooVMNetwork1-Chicago, con le impostazioni seguenti hello.


**Macchina virtuale** | **Rete tooVM connesso**
---|---
VM1 | VMNetwork1-Network
VM2 (replica di VM1) | VMNetwork1-Chicago

Con queste impostazioni esaminare cosa accade in un paio di scenari possibili.

**Scenario** | **Risultato**
---|---
Nessuna modifica apportata alle proprietà di rete hello di VM-2 dopo il failover. | VM-1 rimane connessa toohello rete di origine.
Le proprietà di rete di VM-2 cambiano dopo il failover e la macchina virtuale viene disconnessa  | VM-1 viene disconnessa
Le proprietà di rete di VM-2 vengono modificate dopo il failover e viene connesso tooVMNetwork2-Chicago. | Se non viene eseguito il mapping di VMNetwork2-Chicago, VM-1 verrà disconnessa
Il mapping di rete di VMNetwork1-Chicago viene modificato | VM-1 verrà connessa toohello rete ora mappato tooVMNetwork1-Chicago.



## <a name="next-steps"></a>Passaggi successivi

Informazioni su [pianificazione dell'infrastruttura di rete hello](site-recovery-network-design.md).
