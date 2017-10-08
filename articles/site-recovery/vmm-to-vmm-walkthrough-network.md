---
title: servizi di rete per Hyper-V replica tooa VMM sito secondario con Azure Site Recovery aaaPlan | Documenti Microsoft
description: Questo articolo illustra la pianificazione di rete durante la replica delle macchine virtuali Hyper-V tooa System Center VMM sito secondario con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Passaggio 3: Pianificare la rete per macchina virtuale Hyper-V replica tooa VMM del sito secondario

Dopo aver esaminato i prerequisiti per la distribuzione, leggere questo articolo di tooplan rete quando la replica delle macchine virtuali di Hyper-V (VM) gestite nei cloud di System Center Virtual Machine Manager (VMM), utilizzo del sito secondario tooa [diAzureSiteRecovery](site-recovery-overview.md) in hello portale di Azure. 

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Panoramica del mapping di rete

Mapping di rete viene utilizzato la replica Data Center secondario tooa di macchine virtuali Hyper-V (gestito in VMM). Il mapping di rete esegue il mapping tra reti VM in un server VMM di origine e reti VM in un server VMM di destinazione. Mapping hello seguenti:

- **Connessione di rete**, ovvero le reti di macchine virtuali si connette tooappropriate dopo il failover. replica di Hello VM verrà connesso toohello rete di destinazione di rete di origine mappata toohello.
- **Durante il posizionamento**, in modo ottimale decimali hello macchine virtuali di replica nel server host Hyper-V. Macchine virtuali di replica vengono posizionate in host che possono hello accesso alle reti VM mappate.
- **Nessun mapping di rete**, se non si configura il mapping di rete, le macchine virtuali di replica non sarà le reti VM tooany connesse dopo il failover.


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



## <a name="prepare-for-network-mapping"></a>Preparare il mapping di rete

1. Su hello origine e destinazione server VMM, è necessario disporre di una rete logica associata al cloud di origine e destinazione hello. 
2. Nel server di origine e destinazione hello, è necessario disporre di una rete logica di rete collegati toohello macchina virtuale.
3. Macchine virtuali in host Hyper-V nel percorso di origine hello devono essere collegato toohello rete VM di origine. Se si utilizza solo un singolo server VMM, è possibile configurare il mapping tra le reti VM hello stesso server.

Di seguito è riportato ciò che accede se si configura il mapping di rete durante la distribuzione di Site Recovery:

- Quando si imposta il mapping di rete e selezionare una rete VM di destinazione, verrà visualizzato cloud di origine VMM hello che utilizzano una rete VM di origine hello, insieme a reti VM di destinazione disponibili hello nel cloud di destinazione hello.
- - Quando il mapping è configurato correttamente e la replica è abilitata, una macchina virtuale di origine sarà connessa tooits rete VM di origine e la replica nel percorso di destinazione hello verrà connessa tooits eseguito il mapping di rete VM.
- Se la rete di destinazione hello ha più subnet e una di queste subnet hello stesso nome come hello subnet in cui hello macchina virtuale di origine si trova quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se è presente alcuna subnet di destinazione con un nome corrispondente, hello macchina virtuale sarà connessa toohello prima subnet nella rete hello.

## <a name="connect-toovms-after-failover"></a>Connettere tooVMs dopo il failover

Quando si pianifica la replica e la strategia di failover, una delle domande chiave hello è come tooconnect toohello replica dopo il failover. Vi sono due possibilità: 

- **Utilizzare un indirizzo IP diverso**: È possibile selezionare toouse un indirizzo IP diverso per hello replicati macchina virtuale. In questo hello scenario VM Ottiene un nuovo indirizzo IP dopo il failover ed è richiesto un aggiornamento DNS.
- **Mantenere hello stesso indirizzo IP**: potrebbe essere necessario toouse hello stesso indirizzo IP per la replica hello macchina virtuale. Conservazione hello stessi indirizzi IP semplifica il ripristino di hello riducendo i problemi di rete dopo il failover. 

## <a name="retain-ip-addresses"></a>Mantenere gli indirizzi IP

Se si desidera che gli indirizzi IP di hello tooretain dal sito primario di hello dopo il sito secondario toohello di failover, è possibile eseguire un failover completo subnet e aggiornare le route tooindicate hello nuovo percorso di indirizzi IP hello o alternativa distribuire una subnet tra hello estesa primario e hello siti di ripristino.

### <a name="stretched-subnet"></a>Subnet estesa

In una subnet, con estensione subnet hello è disponibile contemporaneamente in entrambi sito primario e secondario di hello. Se si sposta un server e il relativo sito secondario di configuration toohello IP (livello 3), rete hello indirizzerà nuovo percorso di hello traffico toohello automaticamente. 

Dalla prospettiva del livello 2 (data-link layer), è necessario disporre di apparecchiature di rete in grado di gestire una VLAN estesa. Inoltre, dall'estensione hello VLAN, il dominio di errore potenziali hello estende siti tooboth, diventando essenzialmente un singolo punto di errore. Tuttavia, l'eventualità di una broadcast storm impossibile da isolare è alquanto improbabile. 


### <a name="subnet-failover"></a>Failover sulla subnet

È possibile eseguire un hello tooobtain di failover su subnet vantaggi della subnet hello estesa, senza effettivamente l'estensione. In questa soluzione, una subnet sarà disponibile nel sito di origine o destinazione hello, ma non entrambi contemporaneamente. toomaintain hello spazio degli indirizzi IP nell'evento hello di un failover, è possibile disporre a livello di programmazione per le subnet hello router infrastruttura toomove hello da un sito tooanother. Dopo il quando si verifica il failover, le subnet sposterebbe con hello associato macchine virtuali. svantaggio Hello è che in caso di hello di un errore, si dispone di toomove hello intera subnet.

### <a name="example"></a>Esempio

Di seguito è riportato un esempio di failover su subnet completo. sito primario di Hello dispone di applicazioni in esecuzione in 192.168.1.0/24 subnet. In caso di failover, hello tutte le macchine virtuali in questa subnet viene eseguito il failover del sito secondario toohello e conservare gli indirizzi IP. Route necessità toobe modificato dei fatti hello tooreflect tutte hello VM le macchine virtuali appartenenti toosubnet 192.168.1.0/24 che sono spostati toohello di sito secondario.

Hello seguenti grafici mostrano subnet hello prima e dopo il failover:

- Prima del failover, 192.168.0.1/24 subnet è attivo nel sito di origine hello, diventano attive nel sito secondario hello dopo il failover.
- Hello instrada tra sito primario e sito di ripristino, terzo sito e del sito primario e sito terzo e il sito di ripristino avrà toobe modificate in modo appropriato.

**Prima del failover**

![Prima del failover](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Dopo il failover**

![Dopo il failover](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Di seguito è illustrato ciò che accade dopo il failover:

- Il ripristino del sito alloca un indirizzo IP per ogni interfaccia di rete nella macchina virtuale, hello da hello pool indirizzi IP statici nella rete pertinente hello, per ogni istanza VMM.
- Se il pool di indirizzi IP hello nel sito secondario hello è uguale a quello nel sito di origine hello, il ripristino del sito alloca hello hello stessa replica toohello di indirizzo (della macchina virtuale di origine hello) IP VM. indirizzo IP di Hello è riservato in VMM, ma non è impostato come indirizzo IP di failover hello in host Hyper-V hello. indirizzo IP di failover Hello in un host Hyper-v è stata impostata solo prima del failover hello.
- Se hello stesso indirizzo IP non è disponibile, il ripristino del sito alloca un altro indirizzo IP disponibile dal pool hello.
- Se le macchine virtuali utilizzano DHCP, il ripristino del sito non gestisce gli indirizzi IP hello. È necessario toocheck che hello DHCP server nel sito secondario hello possibile allocare l'indirizzo da hello stesso intervallo come sito di origine hello.

### <a name="validate-hello-ip-address"></a>Convalidare l'indirizzo IP hello

Dopo aver abilitato la protezione per una macchina virtuale, è possibile utilizzare seguente script di esempio tooverify hello indirizzo assegnato toohello macchina virtuale. Hello stesso indirizzo IP verrà impostato come indirizzo IP di failover hello e assegnato toohello VM al momento di hello di failover:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>Modifica degli indirizzi IP

In questo scenario, vengono modificati gli indirizzi IP hello di macchine virtuali di cui eseguire il failover. svantaggio Hello di questa soluzione è manutenzione hello richiesta. In genere, DNS verrà aggiornato dopo l'avvio delle macchine virtuali di replica. Le voci DNS potrebbe essere necessario toobe modificato o fluster in rete e le voci memorizzate nella cache aggiornate. Ciò può comportare tempi di inattività. Il tempo di inattività può essere contrastato come indicato di seguito:

- Usare valori TTL bassi per le applicazioni Intranet.
- Utilizzare lo script seguente in un piano di ripristino di Site Recovery, tooupdate hello DNS server tooensure un aggiornamento tempestivo hello. Se si utilizza la registrazione dinamica DNS non è necessario script hello.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Esempio 

Esaminiamo uno scenario in cui si sta pianificando toouse diversi indirizzi IP tra hello primario e siti di ripristino di hello. In questo esempio sono disponibili diversi indirizzi IP in siti primari e secondari e; s un terzo da cui le applicazioni ospitate nel sito primario o di ripristino di hello possibile accedere al sito.

- Prima del failover, le app sono 192.168.1.0/24 subnet ospitata nel sito primario di hello e sono toobe configurate in subnet 172.16.1.0/24 nel sito secondario hello dopo un failover.
- La configurazione dei percorsi di rete o delle connessioni VPN è avvenuta in modo corretto, pertanto tutti e tre i siti dispongono dell'accesso reciproco.
- Dopo il failover, verranno ripristinate nella subnet ripristino hello app. In questo scenario non c'è alcuna necessità toofail sull'intera subnet hello e modifiche non sono necessari tooreconfigure VPN o rete route. failover Hello e alcuni aggiornamenti DNS, verificare che le applicazioni rimangano accessibili.
- Se gli aggiornamenti dinamici tooallow configurato il DNS, quindi le macchine virtuali hello effettueranno la registrazione mediante hello nuovo indirizzo IP, quando vengono avviati dopo il failover.

**Prima del failover**

![Indirizzo IP diverso - Prima del failover](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Dopo il failover**

![Indirizzo IP diverso - Dopo il failover](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 4: preparare VMM e Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


