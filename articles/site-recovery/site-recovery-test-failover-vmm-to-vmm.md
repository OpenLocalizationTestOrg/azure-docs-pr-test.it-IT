---
title: failover aaaTest (tooVMM VMM) in Azure Site Recovery | Documenti Microsoft
description: Azure Site Recovery coordina la replica di hello, failover e il ripristino delle macchine virtuali e server fisici. Informazioni su failover tooAzure o un Data Center secondario.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Il test di failover (tooVMM VMM) in Site Recovery


Questo articolo contiene informazioni e istruzioni per eseguire un failover di test o un'esercitazione per il ripristino di emergenza di macchine virtuali (VM) e server fisici protetti con Azure Site Recovery. Utilizzare un sito di System Center Virtual Machine Manager VMM gestito in locale come sito di ripristino hello.

Si esegue un toovalidate di failover di test la strategia di replica o esegue un ripristino di emergenza senza alcuna perdita di dati o il tempo di inattività. Un failover di test non hanno alcun impatto sulla replica in corso di hello o nell'ambiente di produzione. È possibile eseguirlo in una macchina virtuale o in un [piano di ripristino](site-recovery-create-recovery-plans.md). Quando si è attivato un failover di test, è necessario rete hello toospecify che si connetterà hello macchine virtuali di test. È possibile analizzare lo stato di avanzamento hello hello del test del failover sul hello **processi** pagina.  

Se si dispone di commenti o domande, pubblicare un post nella parte inferiore di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Preparare l'infrastruttura di hello per il failover di test
Se si desidera toorun un failover di test tramite una rete esistente, preparare Active Directory, DHCP e DNS in tale rete.

Se si desidera toorun un failover di test usando le reti VM di hello opzione toocreate automaticamente, è possibile aggiungere un passaggio manuale prima di Group-1 nel piano di ripristino hello che si userà toouse per il failover di test hello. Aggiungere quindi hello toohello di risorse di infrastruttura creata automaticamente una rete prima di eseguire il failover di test hello.

### <a name="things-toonote"></a>Operazioni toonote
Quando si esegue la replica di tooa sito secondario, il tipo di hello di rete che utilizza hello macchina non deve necessariamente tipo hello toomatch di rete logica utilizzata per il failover di test, ma alcune combinazioni potrebbero non funzionare. Se la replica hello utilizza DHCP e l'isolamento basato su VLAN, la rete VM hello per replica hello non è necessario un pool di indirizzi IP statici. Quindi utilizza la virtualizzazione di rete di Windows per il failover di test hello non funziona perché nessun pool di indirizzi è disponibile. 

Inoltre, il failover di test hello non funziona se rete replica hello non utilizza nessun isolamento e la rete di test hello utilizza la virtualizzazione di rete di Windows. Questo avviene perché rete Nessun isolamento hello privo di hello subnet obbligatorio toocreate una rete di virtualizzazione rete Windows.

Come macchine virtuali di replica sono le reti VM toomapped connesse dopo il failover dipende dalla configurazione di rete VM hello nella console VMM hello.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Rete VM configurata senza isolamento o isolamento VLAN
Se per la rete VM hello è definito DHCP, macchina virtuale di replica hello è connesso toohello ID VLAN tramite le impostazioni di hello specificati per il sito di rete hello nella rete logica associata hello. macchina virtuale Hello riceve il proprio indirizzo IP dal server DHCP disponibile hello. 

Non è necessario toodefine un pool di indirizzi IP statici per la rete VM di destinazione hello. Se un pool di indirizzi IP statici viene utilizzato per la rete VM hello, macchina virtuale di replica hello è connesso toohello ID VLAN tramite le impostazioni di hello specificati per il sito di rete hello nella rete logica associata hello.

macchina virtuale Hello riceve l'indirizzo IP da pool di hello è definito per la rete VM hello. Se nella rete VM di destinazione hello non è definito un pool di indirizzi IP statici, l'allocazione di indirizzi IP avrà esito negativo. Creare il pool di indirizzi IP hello in entrambi hello origine e destinazione VMM i server che verrà utilizzato per la protezione e ripristino.

#### <a name="vm-network-with-windows-network-virtualization"></a>Rete VM con virtualizzazione rete Windows
Se una rete VM è configurata con virtualizzazione rete Windows, è necessario definire un pool statico per la rete VM di destinazione hello, indipendentemente dalla rete VM di origine hello toouse configurato DHCP o un pool di indirizzi IP statici. 

Se si definisce DHCP, server VMM di destinazione hello funge da server DHCP e fornisce un indirizzo IP da pool di hello è definito per la rete VM di destinazione hello. Se per il server di origine hello è definita utilizzo di un pool di indirizzi IP statici, il server VMM di destinazione hello alloca un indirizzo IP dal pool hello. In entrambi i casi, l'allocazione di indirizzi IP non riuscirà se non è definito un pool di indirizzi IP statici.


### <a name="prepare-dhcp"></a>Preparare DHCP
Macchine virtuali hello coinvolte nel failover di test utilizzano DHCP, creare un server DHCP di test all'interno di rete isolata di hello scopo hello di failover di test.

### <a name="prepare-active-directory"></a>Preparare Active Directory
toorun un failover di test per test dell'applicazione, è necessario una copia dell'ambiente Active Directory di produzione hello nell'ambiente di test. Per ulteriori informazioni, esaminare hello [considerazioni sul failover per Active Directory di test](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>Preparare DNS
Preparare un server DNS per il failover di test hello come segue:

* **DHCP**: se le macchine virtuali utilizzano DHCP, aggiornare l'indirizzo IP hello del test di hello DNS sul server DHCP di prova hello. Se si utilizza un tipo di rete di virtualizzazione rete Windows, server VMM hello funge da server DHCP hello. Pertanto, l'indirizzo IP hello del DNS deve essere aggiornato in rete di failover di test hello. In questo caso, le macchine virtuali hello registrarsi toohello relativo server DNS.
* **Indirizzo statico**: se le macchine virtuali utilizzano un indirizzo IP statico, hello l'indirizzo IP del test di hello server DNS deve essere aggiornato in rete di failover di test. Potrebbe essere necessario tooupdate DNS con indirizzo IP hello hello macchine virtuali di test. È possibile utilizzare lo script di esempio seguente a questo scopo hello:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Eseguire un failover di test
Questa procedura viene descritto come toorun un failover di test per il ripristino di un piano. In alternativa, è possibile eseguire failover hello per una singola macchina virtuale in hello **macchine virtuali** scheda.

![Pannello Failover di test](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Selezionare **Piani di ripristino** > *nome_pianodiripristino*. Fare clic su **Failover** > **Test Failover**.
1. In hello **Test Failover** pannello, specificare come macchine virtuali devono essere connessi toonetworks dopo il failover di test hello. Per ulteriori informazioni, vedere hello [Opzioni rete](#network-options-in-site-recovery).
1. Avanzamento di failover su hello **processi** scheda.
1. Al termine del failover, verificare che le macchine virtuali hello avviata correttamente.
1. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note**, registrare e salvare eventuali commenti associati hello test failover. Questo passaggio Elimina hello le macchine virtuali e reti che sono state create durante il failover di test.


## <a name="network-options-in-site-recovery"></a>Opzioni di rete in Site Recovery

Quando si esegue un failover di test, verrà chiesto tooselect le impostazioni di rete per macchine virtuali di replica di test. Sono disponibili varie opzioni.  

| **Opzione di failover di test** | **Descrizione** | **Controllo del failover** | **Dettagli** |
| --- | --- | --- | --- |
| **Eseguire il failover tooa VMM del sito secondario, senza rete** |Non selezionare una rete VM. |Il failover controlla che le macchine di test vengono create.<br/><br/>macchina virtuale di test Hello viene creata nell'host di hello in cui è presente hello macchina virtuale di replica. Non viene aggiunta cloud toohello hello macchina virtuale di replica in cui si trova. |<p>computer failover Hello non è connesso tooany rete.<br/><br/>è possibile rete VM tooa connesso macchina Hello dopo che è stato creato. |
| **Eseguire il failover tooa VMM del sito secondario, con la rete** |Selezionare una rete VM esistente. |Il failover controlla che le macchine virtuali vengano create. |macchina virtuale di test Hello viene creata nell'host di hello in cui è presente hello macchina virtuale di replica. Non viene aggiunta cloud toohello hello macchina virtuale di replica in cui si trova.<br/><br/>Creare una rete VM isolata dalla rete di produzione.<br/><br/>Se si vuole usare una rete basata su VLAN, è consigliabile creare a questo scopo in VMM una rete logica separata non usata in produzione. Questa rete logica è reti VM toocreate utilizzato per i test failover.<br/><br/>rete logica Hello deve essere associata almeno una delle schede di rete hello di tutti i server Hyper-V hello che ospitano macchine virtuali.<br/><br/>Per le reti logiche VLAN, hello siti della rete aggiunti toohello di rete logica devono essere isolati.<br/><br/>Se si usa una rete logica basata su Virtualizzazione rete Windows, Azure Site Recovery crea automaticamente reti VM isolate. |
| **Esito negativo nel corso del sito VMM secondario tooa - creare una rete** |Viene creata automaticamente in base hello all'impostazione specificata in una rete di test temporanea **rete logica** e i relativi siti di rete correlati. |Il failover controlla che le macchine virtuali vengano create. |Utilizzare questa opzione se il piano di ripristino hello utilizza più di una rete VM. Se si utilizzano le reti di virtualizzazione rete Windows, questa opzione potrà creare automaticamente reti VM con hello stesse impostazioni (subnet e pool di indirizzi IP) in rete hello della macchina virtuale di replica hello. Tali reti VM vengono pulite automaticamente dopo il failover di test hello è stato completato.</p><p>macchina virtuale di test Hello viene creata nell'host di hello in cui è presente hello macchina virtuale di replica. Non viene aggiunta cloud toohello hello macchina virtuale di replica in cui si trova. |

> [!TIP]
> indirizzo IP assegnato macchina virtuale tooa durante il test failover Hello è hello riceverebbe stesso indirizzo IP che hello macchina virtuale per un failover pianificato o non pianificato (presumendo che che l'indirizzo IP hello è disponibile in rete di failover di test hello). Se hello stesso indirizzo IP non è disponibile in rete di failover di test hello, macchina virtuale hello riceve un altro indirizzo IP disponibile in rete di failover di test hello.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Rete di produzione tooa di failover di test in un sito di ripristino
Per un failover di test è consigliabile scegliere una rete diversa dalla rete del sito di ripristino di produzione specificata in [Mapping di rete](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Ma se si vuole toovalidate connettività di rete end-to-end in una macchina virtuale con failover, tieni presente hello seguenti punti:

* Assicurarsi che la macchina virtuale primaria hello viene arrestata quando si sta eseguendo il failover di test hello. In caso contrario, due macchine virtuali con hello stessa identità verrà eseguita nella stessa rete in hello hello stesso tempo. Questa situazione può provocare conseguenze tooundesired.
* Le modifiche apportate a toohello test failover delle macchine virtuali vengono perse quando si pulizia hello test failover delle macchine virtuali. Queste modifiche non sono macchina virtuale primaria replicati toohello indietro.
* In questo modo di esecuzione di test viene toodowntime per l'applicazione di produzione. Chiedere agli utenti di un'applicazione hello non toouse applicazione hello quando eseguire il drill-hello ripristino di emergenza è in corso.  


## <a name="next-steps"></a>Passaggi successivi
Dopo l'esito positivo di un failover di test è possibile provare a eseguire un [failover](site-recovery-failover.md).
