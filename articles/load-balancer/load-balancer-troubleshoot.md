---
title: aaaTroubleshoot bilanciamento del carico di Azure | Documenti Microsoft
description: Risolvere i problemi noti di Azure Load Balancer
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Risolvere i problemi di Azure Load Balancer

Questa pagina fornisce informazioni sulla risoluzione dei problemi comuni di Azure Load Balancer. Quando non è disponibile connettività di bilanciamento del carico hello, sintomi di hello più comuni sono i seguenti: 
- Macchine virtuali dietro bilanciamento del carico non rispondono toohealth probe hello 
- Macchine virtuali dietro hello bilanciamento del carico non rispondono toohello traffico sulla porta hello configurato

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Sintomo: Le macchine virtuali dietro hello bilanciamento del carico non rispondono toohealth probe
Per hello tooparticipate server di back-end nel set di bilanciamento carico di hello, passano il controllo di probe hello. Per altre informazioni sui probe di integrità, vedere [Informazioni sui probe di bilanciamento del carico](load-balancer-custom-probe-overview.md). 

pool back-end di bilanciamento del carico Hello macchine virtuali non risponde probe toohello scadenza tooany di hello seguenti motivi: 
- La macchina virtuale del pool back-end di Load Balancer non è integra 
- Macchina virtuale non è in ascolto sulla porta probe hello pool di back-end bilanciamento del carico 
- Firewall o un gruppo di sicurezza di rete blocca la porta hello in hello pool back-end di bilanciamento del carico macchine virtuali 
- Altri errori di configurazione in Load Balancer

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Causa 1: la macchina virtuale del pool back-end di Load Balancer non è integra 

**Convalida e la risoluzione**

tooresolve questo problema, accedere toohello che fanno parte delle macchine virtuali e controllare se hello stato della macchina virtuale è integro e può rispondere troppo**PsPing** o **TCPing** da un'altra macchina virtuale nel pool di hello. Se hello VM non è integro o è Impossibile toorespond toohello probe, è necessario risolvere il problema di hello e ottenere hello VM nuovamente tooa integro prima di poter partecipare bilanciamento del carico.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Causa 2: Pool back-end di bilanciamento del carico macchina virtuale non è in ascolto sulla porta probe hello
Se hello macchina virtuale è integro, ma non risponde toohello probe, uno dei possibili motivi possibile che la porta probe hello non è aperta nel hello che fanno parte di macchina virtuale o hello VM non è in ascolto su tale porta.

**Convalida e la risoluzione**

1. L'accesso back-end toohello macchina virtuale. 
2. Aprire un prompt dei comandi ed eseguire hello è un'applicazione in ascolto sulla porta probe hello toovalidate di comando seguente:   
            netstat -an
3. Se lo stato della porta hello non è elencato come **ascolto**, configurare la porta corretta hello. 
4. In alternativa, selezionare un'altra porta che sia elencata come **LISTENING** e aggiornare la configurazione di Load Balancer di conseguenza.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>Causa 3: Firewall o un gruppo di sicurezza di rete sta bloccando la porta hello nel pool back-end di bilanciamento del carico hello macchine virtuali  
Se firewall hello hello che VM sta bloccando la porta probe hello o uno o più gruppi di sicurezza di rete configurati in subnet hello o in hello macchina virtuale, non è consentita la porta hello tooreach probe di hello, hello VM è Impossibile toorespond toohello probe di integrità.          

**Convalida e la risoluzione**

* Se è abilitato il firewall hello, controllare se viene configurato la porta probe hello tooallow. In caso contrario, configurare il traffico di hello firewall tooallow sulla porta probe hello e provare di nuovo. 
* Elenco hello dei gruppi di sicurezza di rete, controllare se il traffico in ingresso o in uscita hello sulla porta probe hello dispone di un'interferenza. 
* Inoltre, verificare se un **Deny All** regola in hello NIC di hello VM o hello subnet con una priorità maggiore regola predefinita hello che consente le ricerche LB & traffico di gruppi di sicurezza di rete (gruppi di sicurezza di rete devono consentire l'indirizzo IP di bilanciamento del carico di 168.63.129.16). 
* Se uno qualsiasi di queste regole stanno bloccando il traffico di probe hello, rimuovere e riconfigurare il traffico probe hello regole tooallow hello.  
* Verificare se hello VM iniziate risponde probe di integrità toohello. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>Causa 4: altri errori di configurazione in Load Balancer
Se tutti hello cause precedente sembrano toobe convalidare e risolvere correttamente e back-end hello VM ancora non rispondere toohello probe di integrità, quindi manualmente verificare la connettività e raccogliere alcuni connettività hello toounderstand di tracce.

**Convalida e la risoluzione**

* Utilizzare **Psping** da uno dei hello altre macchine virtuali all'interno di hello risposta porta di rete virtuale tootest hello probe (esempio:.\psping.exe -t 10.0.0.4:3389) e registrare i risultati. 
* Utilizzare **TCPing** da uno dei hello altre macchine virtuali all'interno di hello risposta porta di rete virtuale tootest hello probe (esempio:.\tcping.exe 10.0.0.4 3389) e registrare i risultati. 
* Se non si ricevono risposte con questi test di ping:
    - Eseguire un simultanee Netsh di traccia nel pool back-end di destinazione hello VM e un'altra macchina virtuale di test da hello stessa rete virtuale. A questo punto, eseguire un test PsPing per un certo tempo, raccogliere alcune tracce di rete e quindi arrestare il test di hello. 
    - Analizzare l'acquisizione di rete hello e verificare se sono disponibili sia query ping toohello correlati di pacchetti in ingresso e in uscita. 
        - Se i pacchetti in ingresso non vengono rispettati nel pool back-end hello VM, è potenzialmente il traffico hello che causano il blocco di UDR configurazione errata o gruppi di sicurezza di rete. 
        - Se i pacchetti in uscita non vengono rispettati nel pool back-end hello VM, hello VM deve toobe selezionata per i problemi non correlati (per eample, porta probe hello di blocco dell'applicazione). 
    - Verificare se i pacchetti hello probe vengono destinazione tooanother forzato (possibilmente tramite impostazioni UDR) prima di raggiungere un bilanciamento del carico hello. Ciò può provocare hello traffico toonever reach hello back-end macchina virtuale. 
* Modificare (ad esempio, HTTP tooTCP) di tipo probe hello e configurare porta corrispondente di hello in gruppi di sicurezza ACL di rete e firewall toovalidate se è possibile hello problema con la configurazione di hello della risposta di probe. Per altre informazioni sulla configurazione del probe di integrità, vedere la [configurazione del probe di integrità di bilanciamento del carico con endpoint](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Sintomo: Le macchine virtuali di bilanciamento del carico non rispondono tootraffic sulla porta dati hello configurato

Se un macchina virtuale di pool back-end è elencato come integri e risponde toohello probe di integrità, ma ancora non si trova in hello bilanciamento del carico o non risponde toohello il traffico di dati, potrebbe essere dovuto tooany di hello seguenti motivi: 
* Macchina virtuale non è in ascolto sulla porta dati hello pool di back-end del servizio di bilanciamento carico 
* Il gruppo di sicurezza di rete blocca la porta hello in hello pool back-end di bilanciamento del carico macchina virtuale  
* L'accesso a hello bilanciamento del carico da hello stessa macchina virtuale e scheda di rete 
* Accesso hello VIP di bilanciamento del carico Internet da hello che fanno parte di pool back-end di bilanciamento del carico macchina virtuale 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>Causa 1: Pool back-end di bilanciamento del carico macchina virtuale non è in ascolto sulla porta dati hello 
Se una macchina virtuale non risponde toohello il traffico di dati, è possibile che la porta di destinazione hello non è aperta nel hello che fanno parte di macchina virtuale, oppure hello VM non è in ascolto su tale porta. 

**Convalida e la risoluzione**

1. L'accesso back-end toohello macchina virtuale. 
2. Aprire un prompt dei comandi ed eseguire hello è un'applicazione in ascolto sulla porta dati hello toovalidate di comando seguente:  
            netstat -an 
3. Se la porta di hello non è elencata con stato "Ascolto", configurare una porta di listener corretto hello 
4. Se la porta hello è contrassegnata come ascolto, controllare applicazione di destinazione hello su tale porta per i possibili problemi. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Causa 2: Gruppo di sicurezza di rete blocca la porta hello in hello pool back-end di bilanciamento del carico macchina virtuale  

Se uno o più gruppi di sicurezza configurati nella subnet hello hello VM o di rete, sta bloccando hello IP di origine o di porta, quindi VM hello è Impossibile toorespond.

* Elenco di gruppi di sicurezza di rete hello configurati nel back-end hello macchina virtuale. Per altre informazioni, vedere:
    -  [Gestire gruppi di sicurezza di rete utilizzando hello portale](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Gestire i gruppi di sicurezza di rete usando PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* Elenco di hello dei gruppi di sicurezza di rete, verificare se:
    - il traffico in ingresso o in uscita Hello sulla porta dati hello dispone di un'interferenza. 
    - un **Deny All** regola gruppo di sicurezza di rete su hello NIC di subnet VM o hello hello che ha una priorità superiore di tale regola predefinita hello che consente il traffico e probe di bilanciamento del carico (gruppi di sicurezza di rete devono consentire l'indirizzo IP di bilanciamento del carico di 168.63.129.16, che è la porta probe) 
* Se una delle regole di hello stanno bloccando il traffico di hello, rimuovere e riconfigurare il traffico dati hello tooallow tali regole.  
* Verificare se hello VM iniziate toorespond toohello probe di integrità.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>Causa 3: Accesso hello bilanciamento del carico da hello stessa interfaccia di rete e macchina virtuale 

Se l'applicazione ospitato nel back-end hello VM di bilanciamento del carico tenta tooaccess un'altra applicazione ospitata in hello back-end stessa VM su hello stessa interfaccia di rete, è uno scenario non supportato e avrà esito negativo. 

**Risoluzione** è possibile risolvere il problema mediante uno dei seguenti metodi hello:
* Configurare macchine virtuali del pool back-end separate per ogni applicazione. 
* Configurare un'applicazione hello in due macchine virtuali NIC in modo che ogni applicazione è stata usi propri interfaccia di rete e indirizzo IP. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>Causa 4: Accede hello VIP di bilanciamento del carico interno da hello che fanno parte di pool back-end di bilanciamento del carico macchina virtuale

Se è configurato un indirizzo VIP di bilanciamento del carico interno all'interno di una rete virtuale e un back-end partecipante hello macchine virtuali tenta tooaccess hello indirizzo VIP servizio di bilanciamento del carico interno, che ha esito negativo. Questo scenario non è supportato.
**Risoluzione** valutare Gateway applicazione o altri toosupport proxy (ad esempio, nginx o haproxy) che tipo di scenario. Per altre informazioni sul gateway applicazione, vedere [Panoramica del gateway applicazione](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Altre acquisizioni di rete
Se si decide di tooopen un caso di supporto, raccogliere le seguenti informazioni per una risoluzione più veloce hello. Scegliere un hello tooperform VM di back-end seguenti test:
- Usare Psping a un back-end hello macchine virtuali all'interno di hello risposta porta di rete virtuale tootest hello probe (esempio: psping 10.0.0.4:3389) e registrare i risultati. 
- Utilizzare TCPing da uno di back-end hello macchine virtuali all'interno di hello risposta porta di rete virtuale tootest hello probe (esempio: psping 10.0.0.4:3389) e registrare i risultati.
- Se viene ricevuta alcuna risposta per i test di ping, eseguire una traccia Netsh simultanea nel back-end hello VM e hello macchina virtuale di test di rete virtuale, mentre viene eseguito PsPing quindi arresta traccia Netsh hello. 
  
## <a name="next-steps"></a>Passaggi successivi

Se hello passaggi precedenti non risolvono il problema di hello, aprire un [ticket di supporto](https://azure.microsoft.com/support/options/).

