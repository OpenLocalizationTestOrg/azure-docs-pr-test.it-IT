---
title: servizi di rete per la replica VMware tooAzure aaaPlan | Documenti Microsoft
description: In questo articolo vengono illustrati pianificazione necessaria per la replica delle macchine virtuali VMware tooAzure di rete
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a>Passaggio 4: Pianificare la rete per la replica tooAzure VMware

Questo articolo riepiloga le considerazioni sulla pianificazione quando la replica locale tooAzure le macchine virtuali VMware tramite hello rete [Azure Site Recovery](site-recovery-overview.md) servizio.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="connect-tooreplica-vms"></a>Connettere le macchine virtuali tooreplica

Quando si pianifica la replica e la strategia di failover, una delle domande chiave hello è come tooconnect toohello macchina virtuale di Azure dopo il failover. Quando si progetta la strategia di rete per la replica di VM di Azure, sono disponibili due opzioni:

- **Utilizzare l'indirizzo IP diverso**: È possibile selezionare toouse un intervallo di indirizzi IP diversi per hello replicati rete VM di Azure. In questo hello scenario VM Ottiene un nuovo indirizzo IP dopo il failover ed è richiesto un aggiornamento DNS.
- **Mantenere stesso indirizzo IP**: potrebbe essere necessario toouse hello stesso intervallo di indirizzi IP a quella del sito primario locale, per hello Azure rete dopo il failover. Conservazione hello stessi indirizzi IP semplifica il ripristino di hello riducendo i problemi di rete dopo il failover. Tuttavia, quando si esegue la replica tooAzure, sarà necessario route tooupdate con nuovo percorso di hello di indirizzi IP hello dopo il failover. 


## <a name="retain-ip-addresses"></a>Mantenere gli indirizzi IP

Site Recovery fornisce gli indirizzi IP di hello funzionalità tooretain predefinito quando si esegue il failover tooAzure, con un failover su subnet.

Con il failover sulla subnet è presente una subnet specifica nel sito 1 o nel sito 2, ma mai in entrambi i siti contemporaneamente. In ordine toomaintain hello spazio degli indirizzi IP nell'evento hello di un failover, provvederà a livello di codice per le subnet hello router infrastruttura toomove hello da un sito tooanother. Durante il failover, spostamento di subnet hello con hello associate macchine virtuali protette. svantaggio Hello è che in caso di hello di un errore, si dispone di toomove hello intera subnet.


### <a name="failover-example"></a>Esempio di failover

Esaminiamo un esempio di tooAzure di failover.

- Una società fittizia, Woodgrove Bank, dispone di un'infrastruttura locale che ospita le app aziendali. Le applicazioni per dispositivi mobili sono ospitate in Azure.
- La connettività tra macchine virtuali di Woodgrove Bank server locali e Azure viene fornita da una connessione (VPN) da sito a sito tra una rete perimetrale locale di hello e hello rete virtuale di Azure.
- Ciò significa VPN che hello virtuale rete aziendale in Azure viene visualizzato come un'estensione della rete locale.
- Woodgrove vuole toouse Site Recovery tooreplicate locale i carichi di lavoro tooAzure.
 - Woodgrove ha toodeal con applicazioni e le configurazioni che dipendono dal livello di codice gli indirizzi IP e pertanto richiede indirizzi IP tooretain per le applicazioni dopo il failover tooAzure.
 - Woodgrove dispone di indirizzi IP assegnati dall'intervallo 172.16.1.0/24, 172.16.2.0/24 tooits risorse in esecuzione in Azure.


Per Woodgrove toobe in grado di tooreplicate tooAzure relative macchine Virtuali mentre mantenendo hello IP indirizzi, ecco le società hello deve toodo:

1. Creare una rete virtuale di Azure Deve essere un'estensione di hello locale rete, in modo che le applicazioni possono eseguire facilmente il failover.
2. Azure consente di tooadd site-to-site VPN connettività inoltre connettività da sito a toopoint toohello le reti virtuali create in Azure.
3. Quando si configura una connessione site-to-site hello, in Azure hello di rete, è possibile indirizzare percorso locale di traffico toohello (rete locale) solo se l'intervallo di indirizzi IP hello è diverso dall'intervallo di indirizzi IP locale hello.
    - Ciò è dovuto al fatto che Azure non supporta le subnet estese. Pertanto, se si dispone di subnet 192.168.1.0/24 locale, è possibile aggiungere 192.168.1.0/24 una rete locale in hello rete di Azure.
    - È previsto poiché Azure non riconosce che non esistono attivi sono macchine virtuali nella subnet hello e subnet hello viene creato per solo il ripristino di emergenza.
    - toobe toocorrectly in grado di routing del traffico da una subnet hello rete di Azure in rete hello e hello rete locale non deve entrare in conflitto.

![Prima del failover sulla subnet](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a>Prima del failover

1. Creare una rete aggiuntiva (ad esempio una rete di ripristino). Rete hello in cui eseguire il failover le macchine virtuali vengono creati.
2. tooensure che hello indirizzo IP per una macchina virtuale viene mantenuta dopo un failover, nella proprietà della macchina virtuale hello > **configura**, specificare tale hello e macchina virtuale locale, scegliere l'indirizzo IP stesso hello **salvare**.
3. Quando hello VM è stato eseguito il failover, Azure Site Recovery assegnerà hello fornito tooit indirizzo IP.

    ![Proprietà di rete](./media/site-recovery-network-design/network-design8.png)

4. Al termine del failover trigger viene attivato e le macchine virtuali hello vengono create in Azure con l'indirizzo IP hello necessario, è possibile connettersi tramite rete toohello un [connessione di rete virtuale tooVnet](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Questa azione può essere eseguita tramite script.
5. Le route necessarie toobe modificate in modo appropriato, tooreflect che 192.168.1.0/24 ha spostato tooAzure.

    ![Dopo il failover sulla subnet](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a>Dopo il failover

Se non si dispone di una rete di Azure come illustrato in precedenza, è possibile creare una connessione VPN da sito a sito tra il sito primario e Azure, dopo il failover.

## <a name="change-ip-addresses"></a>Modificare gli indirizzi IP

Questo [post di blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) spiega come tooset backup hello Azure infrastruttura di rete quando non è necessario tooretain IP indirizzi dopo il failover. Inizia con una descrizione dell'applicazione, è in modalità tooset di rete locale e in Azure e si conclude con informazioni sull'esecuzione di failover.  

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 5: preparare Azure](vmware-walkthrough-prepare-azure.md)
