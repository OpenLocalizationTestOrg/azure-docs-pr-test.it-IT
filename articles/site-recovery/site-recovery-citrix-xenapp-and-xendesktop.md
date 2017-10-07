---
title: "una distribuzione a più livelli di Citrix XenDesktop e informazioni usando Azure Site Recovery aaaReplicate | Documenti Microsoft"
description: Questo articolo viene descritto come tooprotect e ripristinare di distribuzioni di Citrix XenDesktop e informazioni tramite Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Eseguire la replica di una distribuzione Citrix XenApp e XenDesktop multilivello con Azure Site Recovery

## <a name="overview"></a>Panoramica

Citrix XenDesktop è una soluzione di virtualizzazione desktop che consente di recapitare desktop e applicazioni come un ondemand tooany utente del servizio in qualsiasi punto. Con la tecnologia di recapito, FlexCast XenDesktop rapido e sicuro consegnano toousers desktop e applicazioni.
Citrix XenApp non fornisce attualmente funzionalità di ripristino di emergenza.

Una soluzione di ripristino di emergenza valido, deve consentire di modellazione dei piani di ripristino intorno hello sopra architetture di applicazioni complesse e dispongano di hello possibilità tooadd personalizzato passaggi toohandle applicazione mapping tra i vari livelli fornendo un con clic singolo che cattura soluzione nell'evento hello un'emergenza iniziali tooa inferiore RTO.

Questo documento fornisce indicazioni dettagliate per la creazione di una soluzione di ripristino di emergenza per le distribuzioni Citrix XenApp locali in piattaforme Hyper-V e VMware vSphere. Questo documento descrive inoltre come tooperform un failover di test (analisi di ripristino di emergenza) e con i piani di ripristino, le configurazioni supportata di hello e prerequisiti tooAzure di failover non pianificato.


## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di che aver compreso l'esempio hello:

1. [La replica tooAzure una macchina virtuale](site-recovery-vmware-to-azure.md)
1. Come troppo[progettare una rete di ripristino](site-recovery-network-design.md)
1. [Esegue un tooAzure di failover di test](site-recovery-test-failover-to-azure.md)
1. [Eseguire un failover tooAzure](site-recovery-failover.md)
1. Come troppo[replicare un controller di dominio](site-recovery-active-directory.md)
1. Come troppo[la replica di SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modelli di distribuzione

Una farm Citrix XenApp e XenDesktop include in genere hello seguente modello di distribuzione:

**Modello di distribuzione**

Distribuzione Citrix XenApp e XenDesktop con server DNS di AD, server di database SQL, Citrix Delivery Controller, server StoreFront, XenApp Master (VDA), server licenze di Citrix XenApp

![Modello di distribuzione 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Supporto di Site Recovery

A scopo di hello di questo articolo, Citrix le distribuzioni di macchine virtuali VMware è gestito da vSphere 6.0 o System Center VMM 2012 R2 sono stati utilizzati toosetup ripristino di emergenza.

### <a name="source-and-target"></a>Origine e destinazione

**Scenario** | **sito secondario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Non nell'ambito | Sì
**VMware** | Non nell'ambito | Sì
**Server fisico** | Non nell'ambito | Sì

### <a name="versions"></a>Versioni
I clienti possono distribuire componenti di XenApp come macchine virtuali in esecuzione su Hyper-V o VMware oppure come server fisici. Azure Site Recovery può proteggere entrambi tooAzure distribuzioni fisici e virtuali.
Poiché informazioni 7.7 o versioni successive sono supportato in Azure, solo le distribuzioni con tali versioni non consente il failover tooAzure per il ripristino di emergenza o la migrazione.

### <a name="things-tookeep-in-mind"></a>Operazioni tookeep presente

1. Protezione e ripristino di on-premise le distribuzioni con sistema operativo Server macchine toodeliver informazioni App pubblicate e informazioni pubblicate desktop è supportata.

2. Protezione e il ripristino delle distribuzioni locali utilizzando desktop del sistema operativo macchine toodeliver Desktop VDI per i desktop virtuali client, incluso Windows 10, non è supportata. Infatti, ripristino automatico di sistema non supporta il ripristino hello di computer con desktop OS'es.  Alcuni tipi di desktop virtuale client, ad esempio Windows 7, non sono inoltre ancora supportati per le licenze in Azure. [Altre informazioni](https://azure.microsoft.com/pricing/licensing-faq/) sulle licenze per computer desktop client/server in Azure.

3.  Azure Site Recovery non può replicare e proteggere cloni MCS o PVS locali esistenti.
È necessario toorecreate i cloni utilizzando Azure RM provisioning dal controller di recapito.

4. NetScaler non può essere protetto tramite Azure Site Recovery perché NetScaler è basato su FreeBSD e Azure Site Recovery non supporta la protezione del sistema operativo FreeBSD. Si sarebbe necessario toodeploy e configurare un nuovo dispositivo NetScaler da Azure Marketplace dopo il failover tooAzure.


## <a name="replicating-virtual-machines"></a>Replica di macchine virtuali

Hello seguenti componenti di hello Citrix XenApp distribuzione necessario replica tooenable toobe protetto e il ripristino.

* Protezione del server DNS di AD
* Protezione del server di database SQL
* Protezione di Citrix Delivery Controller
* Protezione del server StoreFront
* Protezione di XenApp Master (VDA)
* Protezione del server licenze di Citrix XenApp


**Replica del server DNS di AD**

Consultare troppo[proteggere Active Directory e DNS con Azure Site Recovery](site-recovery-active-directory.md) alle linee guida per la replica e la configurazione di un controller di dominio in Azure.

**Replica del server di database SQL**

Consultare troppo[proteggere SQL Server con il ripristino di emergenza di SQL Server e Azure Site Recovery](site-recovery-sql.md) per indicazioni tecniche dettagliate su hello consigliabile opzioni per la protezione di SQL Server.

Seguire [questa Guida](site-recovery-vmware-to-azure.md) toostart replica hello altri tooAzure di macchine virtuali del componente.

![Protezione dei componenti di XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**Impostazioni di Calcolo e rete**

Dopo che sono protetti macchine hello (stato viene visualizzato come "Protetto" in elementi replicati), hello calcolo e le impostazioni di rete necessario toobe configurato.
Nel calcolo e rete > calcolo proprietà, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione.
Se si desidera, modificare toocomply nome hello ai requisiti di Azure. È inoltre possibile visualizzare e aggiungere le informazioni di rete di destinazione hello, subnet e indirizzi IP che verranno assegnato toohello macchina virtuale di Azure.

Si noti hello segue:

* È possibile impostare l'indirizzo IP di destinazione hello. Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP. Se si imposta un indirizzo che non è disponibile in caso di failover, failover hello non funzionerà. Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.

* Per il server di Active Directory/DNS hello, mantenendo hello locale consente di indirizzo che specificare hello uguale indirizzo come server DNS hello per la rete virtuale di Azure hello.

numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:

*   Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.
*   Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.
* Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede. Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.
*   Se più schede di rete nella macchina virtuale hello verranno tutti connettono toohello stessa rete.
*   Se macchina virtuale hello dispone di più schede di rete, hello primo quello riportato nell'elenco di hello diventa quindi scheda di rete predefinito hello in hello macchina virtuale di Azure.


## <a name="creating-a-recovery-plan"></a>Creazione di un piano di ripristino

Dopo la replica è abilitata per le macchine virtuali componente informazioni hello, hello è toocreate un piano di ripristino.
Un piano di ripristino raggruppa le macchine virtuali con requisiti simili per il failover e il ripristino.  

**Passaggi toocreate un piano di ripristino**

1. Aggiungi macchine virtuali di hello informazioni componente hello il piano di ripristino.
2. Fare clic su Piani di ripristino -> + Piano di ripristino. Fornire un nome per il piano di ripristino hello intuitivo.
3. Per macchine virtuali VMware: selezionare il server di elaborazione VMware come origine, Microsoft Azure come destinazione e Resource Manager come modello di distribuzione, quindi fare clic su Seleziona elementi.
4. Per le macchine virtuali Hyper-V: selezionare l'origine come server VMM, come Microsoft Azure e il modello di distribuzione come Gestione risorse di destinazione e fare clic su selezionare gli elementi e quindi selezionare la distribuzione di informazioni di hello macchine virtuali.

### <a name="adding-virtual-machines-toofailover-groups"></a>Aggiunta di gruppi toofailover macchine virtuali

I piani di ripristino possono essere personalizzato tooadd failover gruppi per le azioni di avvio specifico ordine, script o manuale. Hello seguenti gruppi necessario toobe toohello aggiunto piano di ripristino.

1. Gruppo di failover 1: DNS di AD
2. Gruppo di failover 2: VM SQL Server
2. Gruppo di failover 3: VM di immagine master VDA
3. Gruppo di failover 4: controller di distribuzione e VM del server StoreFront


### <a name="adding-scripts-toohello-recovery-plan"></a>Aggiunta di script toohello piano di ripristino

Gli script possono essere eseguiti prima o dopo un gruppo specifico in un piano di ripristino. È anche possibile includere azioni manuali ed eseguirle durante il failover.

piano di ripristino personalizzata Hello è simile hello riportato di seguito:

1. Gruppo di failover 1: DNS di AD
2. Gruppo di failover 2: VM SQL Server
3. Gruppo di failover 3: VM di immagine master VDA

   >[!NOTE]     
   >I passaggi 4, 6 e 7 contenente azioni manuali o uno script sono applicabili tooonly un informazioni locali > ambiente cataloghi MCS/PV.

4. Azione manuale o script di gruppo 3: hello VDA VM master di arresto Master VDA VM quando è stato eseguito il failover tooAzure sarà in uno stato di esecuzione. toocreate nuovo MCS cataloghi utilizzando Azure ARM hosting, master hello VDA VM è necessario toobe Stopped (de allocato) dello stato. Hello arresto macchina virtuale dal portale di Azure.

5. Gruppo di failover 4: controller di distribuzione e VM del server StoreFront
6. Gruppo 3 - Azione manuale o di script 1:

    ***Aggiungere una connessione host di Azure RM***

    Crea connessione all'host di Azure ARM tooprovision computer Controller di recapito nuovi cataloghi MCS in Azure. Seguire i passaggi di hello, come illustrato in questo [articolo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Gruppo 3 - Azione manuale o di script 2:

    ***Ricreare i cataloghi MCS in Azure***

    Hello esistente MCS o PV cloni nel sito primario di hello non saranno replicate tooAzure. È necessario toorecreate i cloni utilizzando hello replicati VDA master e ARM Azure provisioning dal controller di recapito. Seguire i passaggi di hello, come illustrato in questo [articolo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS cataloghi in Azure.

![Piano di ripristino per i componenti XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >È possibile utilizzare script in [percorso](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS con i nuovi indirizzi IP di hello failover hello > macchine virtuali o tooattach hello un bilanciamento del carico failover macchina virtuale, se necessario.


## <a name="doing-a-test-failover"></a>Esecuzione di un failover di test

Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.

![Piano di ripristino](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Esecuzione di un failover

Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.

## <a name="next-steps"></a>Passaggi successivi

Per [altre informazioni](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sulla replica di distribuzioni Citrix XenApp e XenDesktop, vedere questo white paper. Esaminare indicazioni hello troppo[replicare altre applicazioni](site-recovery-workload.md) utilizzando il ripristino del sito.
