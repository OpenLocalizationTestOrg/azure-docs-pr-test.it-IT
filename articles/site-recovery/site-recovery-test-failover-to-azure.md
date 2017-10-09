---
title: aaaTest failover tooAzure in Site Recovery | Documenti Microsoft
description: Informazioni sull'esecuzione di un failover di test da tooAzure locale
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
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Test Failover tooAzure in Site Recovery



In questo articolo fornisce informazioni e istruzioni per effettuare un failover di test o un ripristino di emergenza delle macchine virtuali e server fisici che sono protetti con il ripristino del sito, usare Azure come sito di ripristino hello.

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Failover di test è toovalidate la strategia di replica oppure eseguire un'analisi di ripristino di emergenza senza alcuna perdita di dati o il tempo di inattività. Effettuare un failover di test non hanno alcun impatto sulla replica in corso di hello o nell'ambiente di produzione. Il failover di test può essere eseguito su una macchina virtuale o un [piano di ripristino](site-recovery-create-recovery-plans.md). Al momento della generazione di un failover di test, è necessario test toowhich rete hello toospecify connessione macchine virtuali. Una volta che viene attivato un failover di test, è possibile monitorare lo stato di avanzamento in hello **processi** pagina.  


## <a name="supported-scenarios"></a>Scenari supportati
Test del failover è supportato in tutti gli scenari di distribuzione diverso da [legacy VMware sito tooAzure](site-recovery-vmware-to-azure-classic-legacy.md). Failover di test non è anche supportato quando la macchina virtuale è stata eseguita in tooAzure.  


## <a name="run-a-test-failover"></a>Eseguire un failover di test
Questa procedura viene descritto come toorun un failover di test per il ripristino di un piano. In alternativa è possibile eseguire anche il failover di test per una singola macchina tramite conveniente hello su di esso.

![Failover di test](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Selezionare **Piani di ripristino** > *nome_pianodiripristino*. Fare clic su **Failover di test**.
1. Selezionare un **punto di ripristino** toofailover per. È possibile utilizzare una delle seguenti opzioni hello:
    1.  **Ultima elaborazione**: questa opzione viene eseguito il failover tutte le macchine virtuali hello piano toohello ultimo ripristino del punto di ripristino che è già stato elaborato dal servizio Site Recovery. Quando si esegue il failover di test di una macchina virtuale, viene visualizzato anche i timestamp dell'ultimo punto di ripristino elaborato hello. Se si esegue il failover di un piano di ripristino, è possibile passare una macchina virtuale tooindividual e osservare **punti di ripristino più recente** riquadro tooget queste informazioni. Come non viene impiegato per l'ora tooprocess hello dati non elaborati, questa opzione offre un'opzione failover RTO (tempo Recovery Time Objective).
    1.  **Versione più recente coerente con app**: questa opzione non funziona su tutte le macchine virtuali di hello piano toohello più recente dell'applicazione ripristino coerenti con punto di ripristino che è già stato elaborato dal servizio Site Recovery. Quando si esegue il failover di test di una macchina virtuale, viene visualizzato anche i timestamp dell'ultimo punto di ripristino coerenti con l'applicazione hello. Se si esegue il failover di un piano di ripristino, è possibile passare una macchina virtuale tooindividual e osservare **punti di ripristino più recente** riquadro tooget queste informazioni.
    1.  **Più recente**: questa opzione Elabora prima tutti i dati che sono stato inviato tooSite ripristino servizio toocreate un punto di ripristino per ogni macchina virtuale prima del failover li tooit hello. Questa opzione offre hello più basso RPO (Recovery Point Objective) come macchina virtuale hello creato dopo il failover disporrà di tutti i dati di hello che è stata replicata tooSite servizio di ripristino quando hello failover è stato attivato.
    1.  **Latest multi-VM processed** (Più recente coerente tra più VM elaborato): questa opzione è disponibile solo per i piani di ripristino con almeno una macchina virtuale in cui è abilitata la coerenza tra più macchine virtuali. Macchine virtuali che fanno parte di un gruppo failover toohello più recente comuni tra più macchine coerente ripristino della replica del punto. Altre macchine virtuali failover tootheir ultimo elaborati punto di ripristino.  
    1.  **Latest multi-VM app-consistent** (Più recente coerente con l'applicazione tra più VM): questa opzione è disponibile solo per i piani di ripristino con almeno una macchina virtuale in cui è abilitata la coerenza tra più macchine virtuali. Macchine virtuali che fanno parte di una replica di tipo gruppo failover toohello ultimo comuni tra più macchine coerenti con l'applicazione punto di ripristino. Altre macchine virtuali failover tootheir più recente coerente con l'applicazione del punto di ripristino. 
    1.  **Custom**: se si sta eseguendo il failover di test di una macchina virtuale, quindi è possibile utilizzare questo punto di recupero specifico tooa toofailover opzione.
1. Selezionare un **rete virtuale di Azure**: fornire una rete virtuale di Azure in cui verrebbe create hello macchine virtuali di test. Il ripristino del sito tenta toocreate macchine virtuali di test in una subnet con stesso nome e con hello stesso IP a quella fornita **di calcolo e rete** impostazioni della macchina virtuale hello. Se non è disponibile nella rete virtuale di Azure fornito per il failover di test, hello subnet stesso nome macchina virtuale di test viene creato nella prima subnet hello in ordine alfabetico. Se lo stesso IP non è disponibile nella subnet hello, macchina virtuale riceve un altro indirizzo IP disponibile nella subnet hello. Per altri dettagli, vedere [questa sezione](#creating-a-network-for-test-failover).
1. Se sta failover tooAzure e data encryption è abilitato in **chiave di crittografia** certificato selezionare hello emesso quando è abilitata la crittografia dei dati durante l'installazione del Provider. È possibile ignorare questo passaggio se non è stata abilitata la crittografia nella macchina virtuale hello.
1. Avanzamento di failover su hello **processi** scheda. Si dovrebbe essere macchina di replica in grado di toosee hello test nel portale di Azure hello.
1. una connessione RDP sulla macchina virtuale hello tooinitiate, sarà necessario troppo[aggiungere un indirizzo ip pubblico](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) su hello interfaccia di rete di hello non riuscita sulla macchina virtuale. Se viene eseguito il failover macchina virtuale di tooa classica, quindi è necessario troppo[aggiungere un endpoint](../virtual-machines/windows/classic/setup-endpoints.md) sulla porta 3389
1. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. In **note** registrare e salvare eventuali commenti associati hello test failover. Vengono eliminate le macchine virtuali hello creati durante il failover di test.


> [!TIP]
> Il ripristino del sito tenta toocreate macchine virtuali di test in una subnet con stesso nome e con hello stesso IP a quella fornita **di calcolo e rete** impostazioni della macchina virtuale hello. Se non è disponibile nella rete virtuale di Azure fornito per il failover di test, hello subnet stesso nome macchina virtuale di test viene creato nella prima subnet hello in ordine alfabetico. Se hello IP di destinazione fa parte di hello scelto subnet, il ripristino del sito tenta di macchina virtuale toocreate hello test failover utilizzando l'indirizzo IP di destinazione hello. Se l'indirizzo IP di destinazione hello non fa parte di hello scelto subnet macchina virtuale di failover di test viene creato utilizzando qualsiasi IP disponibile in hello scelto subnet.
>
>

## <a name="test-failover-job"></a>Processo di failover di test

![Failover di test](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

L'attivazione di un failover di test comporta l'esecuzione dei passaggi riportati di seguito.

1. Verifica preliminare: questo passaggio garantisce che siano soddisfatte tutte le condizioni necessarie per il failover.
1. Failover: Questo passaggio elabora i dati di hello e rende pronti in modo che sia possibile creare esplicitamente una macchina virtuale di Azure. Se si è scelto **più recente** punto di ripristino, questo passaggio Crea un punto di ripristino dai dati di hello inviati toohello servizio.
1. Start: Questo passaggio viene creata una macchina virtuale di Azure utilizzando dati hello elaborati nel passaggio precedente hello.

## <a name="time-taken-for-failover"></a>Tempo impiegato per il failover

In alcuni casi, il failover delle macchine virtuali prevede un passaggio intermedio aggiuntiva che in genere richiede circa 8 too10 minuti toocomplete. Questi casi sono i seguenti:

* Macchine virtuali VMware utilizzando una versione di hello meno recente 9.8 servizio di mobilità
* Server fisici
* Macchine virtuali VMware Linux
* Macchine virtuali Hyper-V protette come server fisici
* Macchine virtuali VMware in cui i driver seguenti non sono presenti come driver di avvio
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* Macchine virtuali VMware che non dispongono del servizio DHCP abilitato indipendentemente che usino indirizzi IP statici o DHCP.

In hello tutti gli altri casi questo passaggio intermedio non è necessario e tempo per il failover hello hello è notevolmente inferiore.


## <a name="creating-a-network-for-test-failover"></a>Creazione di una rete per il failover di test
È consigliabile quando si esegue un failover di test scegliere una rete isolata dalla rete di sito di ripristino di produzione fornito nel **di calcolo e rete** impostazioni per la macchina virtuale hello. Quando si crea una rete virtuale di Azure, per impostazione predefinita è isolata dalle altre reti. La rete dovrà simulare la rete di produzione:

1. Rete di test deve disporre dello stesso numero di subnet a quello della rete di produzione e con hello stesso nome di quelli della subnet hello nella rete di produzione.
1. Rete di test deve utilizzare hello stesso intervallo IP di rete di produzione.
1. Hello aggiornamento DNS della rete di Test come hello IP assegnato come IP di destinazione per la macchina virtuale DNS hello in hello **di calcolo e rete** impostazioni. Per altri dettagli, vedere la sezione [Considerazioni sul failover di test per Active Directory](site-recovery-active-directory.md#test-failover-considerations) .


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Rete di produzione tooa di failover di test nel sito di ripristino
È consigliabile quando si esegue un failover di test scegliere una rete che è diversa dalla rete di sito di ripristino di produzione fornito nel **di calcolo e rete** impostazioni per la macchina virtuale hello. Tuttavia, se si vuole toovalidate di connettività di rete end tooend non riuscita sulla macchina virtuale, si noti hello seguenti punti:

1. Assicurarsi che la macchina virtuale primaria hello viene chiusa quando si esegue il failover di test hello. Se non si configura questo, saranno presenti due macchine virtuali con hello stessa identità in esecuzione in hello stessa rete in hello contemporaneamente e che può comportare conseguenze tooundesired.
1. Tutte le modifiche apportate in hello test failover delle macchine virtuali andrebbero perse quando si pulizia hello test failover delle macchine virtuali. Queste modifiche non saranno macchina virtuale primaria replicati toohello indietro.
1. Questa modalità di esecuzione di test lead tooa i tempi di inattività dell'applicazione di produzione. Agli utenti di un'applicazione hello devono essere richiesto un'applicazione hello utilizzare toonot quando eseguire il drill-hello ripristino di emergenza è in corso.  



## <a name="prepare-active-directory-and-dns"></a>Preparare Active Directory e DNS
toorun un failover di test per test dell'applicazione, è necessario una copia dell'ambiente Active Directory di produzione hello nell'ambiente di test. Per altri dettagli, vedere la sezione [Considerazioni sul failover di test per Active Directory](site-recovery-active-directory.md#test-failover-considerations) .

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Preparazione di macchine virtuali tooAzure tooconnect dopo il failover

Se si desidera tooconnect tooAzure macchine virtuali tramite RDP dopo il failover, assicurarsi che si hello azioni riepilogate nella tabella hello.

**Failover** | **Posizione** | **Actions**
--- | --- | ---
**VM di Azure che esegue Windows** | Nel computer locale prima del failover | tooaccess hello macchina virtuale di Azure tramite internet hello, abilitare RDP, assicurarsi che TCP e UDP regole vengono aggiunte per hello **pubblica**, e che il protocollo RDP è consentito in **Windows Firewall** > **consentiti App**, per tutti i profili.<br/><br/> tooaccess tramite una connessione site-to-site, abilitare RDP nel computer di hello e assicurarsi che il protocollo RDP è consentito in hello **Windows Firewall** -> **consentito App e funzionalità** per  **Dominio e Private** reti.<br/><br/>  Assicurarsi che i criteri di rete SAN del sistema operativo hello sono impostato troppo**OnlineAll**. [Altre informazioni](https://support.microsoft.com/kb/3031135)<br/><br/> Assicurarsi che non sono disponibili aggiornamenti di Windows in sospeso nella macchina virtuale hello quando si avvia un failover. Aggiornamento di Windows potrebbe iniziare quando failover e non sarà macchina virtuale di toologin in grado di toohello fino al completamento dell'aggiornamento hello. <br/><br/>
**VM di Azure che esegue Windows** | Nella VM di Azure dopo il failover | Per una macchina virtuale classica, [aggiungere un endpoint pubblico](../virtual-machines/windows/classic/setup-endpoints.md) per hello protocollo RDP (porta 3389)<br/><br/>  Per una macchina virtuale di Resource Manager, [aggiungere un indirizzo IP pubblico](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) nella macchina virtuale.<br/><br/> Hello regole gruppo di sicurezza di rete sul failover VM hello e hello toowhich subnet di Azure è connesso, è necessario porta RDP toohello tooallow in ingresso connessioni.<br/><br/> Per una macchina virtuale di gestione delle risorse, è possibile verificare **diagnostica di avvio** toolook in una schermata di macchina virtuale hello<br/><br/> Se non è possibile connettersi, verificare che hello macchina virtuale è in esecuzione e quindi esaminare questi [suggerimenti sulla risoluzione dei](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**VM di Azure che esegue Linux** | Nel computer locale prima del failover | Verificare che il servizio di Secure Shell su hello Azure VM hello sia impostato toostart automaticamente all'avvio del sistema.<br/><br/> Controllare che le regole del firewall consentano un tooit connessione SSH.
**VM di Azure che esegue Linux** | VM di Azure dopo il failover | Hello regole gruppo di sicurezza di rete sul failover VM hello e hello toowhich subnet di Azure è connesso, è necessario porta SSH toohello tooallow in ingresso connessioni.<br/><br/> Per una macchina virtuale classica, [aggiungere un endpoint pubblico](../virtual-machines/windows/classic/setup-endpoints.md) deve essere creato, le connessioni in ingresso tooallow su hello SSH (porta TCP 22 per impostazione predefinita).<br/><br/> Per una macchina virtuale di Resource Manager, [aggiungere un indirizzo IP pubblico](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) nella macchina virtuale.<br/><br/> Per una macchina virtuale di gestione delle risorse, è possibile verificare **diagnostica di avvio** toolook in una schermata di macchina virtuale hello<br/><br/>



## <a name="next-steps"></a>Passaggi successivi
Dopo l'esito positivo di un failover di test, si può provare a eseguire un [failover](site-recovery-failover.md).
