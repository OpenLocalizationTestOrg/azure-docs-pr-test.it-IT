---
title: una distribuzione di applicazioni SAP NetWeaver multilivello usando Azure Site Recovery aaaProtect | Documenti Microsoft
description: In questo articolo viene descritto come tooprotect SAP NetWeaver le distribuzioni di applicazioni usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Proteggere una distribuzione di applicazioni SAP NetWeaver multilivello usando Azure Site Recovery

La maggior parte delle distribuzioni SAP di medie e grandi dimensioni prevede una soluzione di ripristino di emergenza.  importanza Hello di soluzioni di ripristino di emergenza efficaci e testabili è aumentato come attività più processi sono spostati tooapplications, ad esempio SAP.  Azure Site Recovery è state testate e integrate con applicazioni SAP e supera la capacità hello della maggior parte delle soluzioni di ripristino di emergenza locale, a un costo totale di proprietà (TCO) rispetto alle soluzioni della concorrenza.
Con Azure Site Recovery è possibile:
* Abilitare la protezione di applicazioni SAP NetWeaver e non di produzione NetWeaver in esecuzione in locale, tramite la replica tooAzure componenti.
* Abilitare la protezione di applicazioni SAP NetWeaver e non di produzione NetWeaver in esecuzione di Azure, grazie alla replica tooanother componenti Data Center di Azure.
* Semplificare la migrazione di cloud, tramite il ripristino del sito toomigrate il tooAzure distribuzione SAP.
* Semplificare gli aggiornamenti, i test e la creazione di prototipi dei progetti SAP, creando un clone di produzione on demand per i test delle applicazioni SAP.

In questo articolo viene descritto come tooprotect SAP NetWeaver le distribuzioni di applicazioni utilizzando [Azure Site Recovery](site-recovery-overview.md). In questo articolo illustra hello le procedure consigliate per la protezione di una distribuzione di SAP NetWeaver a tre livelli in Azure mediante la replica tooanother Data Center di Azure usando Azure Site Recovery, scenari di hello supportato e configurazioni, e come i failover tooperform, entrambi i test failover (analisi di ripristino di emergenza) e failover effettivo.


## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare, assicurarsi di che aver compreso l'esempio hello:

1. [La replica tooAzure una macchina virtuale](azure-to-azure-walkthrough-enable-replication.md)
2. Come troppo[progettare una rete di ripristino](site-recovery-azure-to-azure-networking-guidance.md)
3. [Esegue un tooAzure di failover di test](azure-to-azure-walkthrough-test-failover.md)
4. [Eseguire un failover tooAzure](site-recovery-failover.md)
5. Come troppo[replicare un controller di dominio](site-recovery-active-directory.md)
6. Come troppo[la replica di SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Scenari supportati
Con Azure Site Recovery è possibile implementare una soluzione di ripristino di emergenza per hello seguenti scenari:
* I sistemi SAP in esecuzione in un Data Center di Azure la replica tooanother Data Center di Azure (ripristino di emergenza Azure in Azure), come l'architettura [qui](https://aka.ms/asr-a2a-architecture).
* I sistemi SAP in esecuzione su VMWare o fisici server replica tooa ripristino di emergenza sito locale in un Data Center di Azure (ripristino di emergenza VMware in Azure), che richiede alcuni componenti aggiuntivi, come l'architettura [qui](https://aka.ms/asr-v2a-architecture).
* Sistemi SAP in esecuzione in Hyper-V replica tooa ripristino di emergenza sito locale in un Data Center di Azure (ripristino di emergenza Hyper-V in Azure), che richiede alcuni componenti aggiuntivi, come l'architettura [qui](https://aka.ms/asr-h2a-architecture).

Questo documento usa una funzionalità di ripristino di emergenza SAP hello prima case - ripristino di emergenza di Azure in Azure - toodemonstrate Azure Site Recovery. Come la replica di Azure Site Recovery è indipendente dall'applicazione, il processo di hello descritto è toohold previsto per altri scenari anche.

### <a name="required-foundation-services"></a>Servizi di base necessari
Questo scenario documentazione tutti stato distribuito con i seguenti servizi foundation distribuiti hello:
* ExpressRoute o VPN (rete privata virtuale) da sito a sito
* Almeno un controller di dominio Active Directory e il server DNS in esecuzione in Azure

È consigliabile che l'infrastruttura di hello sopra è stabilita toodeploying precedente Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Distribuzione tipica di un'applicazione SAP
I clienti SAP di grandi dimensioni in genere distribuire tra 6 too20 singoli le applicazioni SAP.  La maggior parte di queste applicazioni sono basata su SAP NetWeaver ABAP o Java motori di hello.  A supporto di queste applicazioni NetWeaver di base ci sono numerosi motori autonomi SAP non NetWeaver più piccoli e in genere alcune applicazioni non SAP.  

È critico tooinventory varianza dimensioni, tutte le applicazioni SAP di hello in esecuzione in una varietà e toodetermine hello modalità di distribuzione (livello 2 o 3 livelli), versioni, patch, frequenze e requisiti di persistenza di disco.

![Modello di distribuzione](./media/site-recovery-sap/sap-typical-deployment.png)

livello di persistenza Database SAP Hello deve essere protetti tramite strumenti DBMS nativi hello, ad esempio AlwaysOn di SQL Server, Oracle DataGuard o replica DFS HANA. livello client Hello anche non protetto da Azure Site Recovery, ma è importante tooconsider argomenti che influiscono su questo livello, ad esempio ritardo di propagazione DNS, sicurezza e accesso remoto toohello Data Center di ripristino di emergenza.

Azure Site Recovery è hello per livello di applicazione hello, tra cui (A) SCS la soluzione consigliata. Altre applicazioni, ad esempio applicazioni non SAP NetWeaver e SAP non fanno parte di hello SAP complessiva ambiente di distribuzione e deve essere protetto anche con Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Replicare le macchine virtuali
Seguire [questa Guida](azure-to-azure-walkthrough-enable-replication.md) toostart replicare tutte hello toohello di macchine virtuali dell'applicazione SAP Azure Data Center di ripristino di emergenza.

Se si utilizza un indirizzo IP statico, è possibile specificare hello IP che si desidera hello tootake macchina virtuale nella sezione di hello Network interface card nelle impostazioni di calcolo e di rete.

![IP di destinazione](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Creazione di un piano di ripristino
Un piano di ripristino consente di sequenziazione failover hello di vari livelli di un'applicazione multilivello, di conseguenza, mantenendo la coerenza delle applicazioni. Seguire i passaggi di hello descritti [qui](site-recovery-create-recovery-plans.md) durante la creazione di un piano di ripristino per un'applicazione web a più livelli.

### <a name="adding-scripts-toohello-recovery-plan"></a>Aggiunta di script toohello piano di ripristino
Potrebbe essere necessario toodo alcune operazioni su macchine virtuali di Azure post failover o test failover hello per le applicazioni toofunction correttamente. È possibile automatizzare l'operazione di failover hello post, ad esempio durante l'aggiornamento voce DNS e la modifica di associazioni e le connessioni, tramite l'aggiunta di script corrispondenti nel piano di ripristino hello come descritto in [questo articolo](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Aggiornamento del DNS
Se hello DNS è configurato per l'aggiornamento dinamico DNS, quindi le macchine virtuali, in genere, aggiornare hello DNS con hello nuovo indirizzo IP quando vengono avviati. Se si desidera tooadd tooupdate un passaggio esplicita DNS con hello nuovi indirizzi IP delle macchine virtuali hello quindi aggiungere questo [script tooupdate IP nel DNS](https://aka.ms/asr-dns-update) come un'azione post su gruppi del piano di ripristino.  

## <a name="example-azure-to-azure-deployment"></a>Esempio di distribuzione da Azure ad Azure
È illustrato nel diagramma hello di sotto di uno scenario di ripristino di emergenza di Azure Site Recovery Azure in Azure hello:
* Hello Data Center principale è Singapore (Asia sudorientale Azure) e Data Center di ripristino di emergenza hello è Hong Kong (Asia orientale di Azure).  In questo scenario, la disponibilità elevata locale viene fornita con due VM che eseguono SQL Server AlwaysOn in modalità sincrona a Singapore.
* Hello ASCS condivisione File può essere utilizzato tooprovide a disponibilità elevata per i singoli punti SAP hello di errore. L'istanza ASCS di condivisione file non richiede un disco condiviso del cluster e le applicazioni, ad esempio SIOS, non sono necessarie.
* Protezione di ripristino di emergenza per il livello DBMS hello viene eseguita mediante la replica asincrona.
* In questo scenario viene "DR simmetrico": utilizzare un termine toodescribe una soluzione di ripristino di emergenza che è una replica esatta di produzione, pertanto hello soluzione di ripristino di emergenza di SQL Server dispone di un'elevata disponibilità locale. uso di Hello del ripristino di emergenza simmetrico non è obbligatorio per il livello di Database hello e molti clienti di sfruttare la flessibilità di hello di distribuzioni di cloud toobuild un nodo di disponibilità elevata locale rapidamente dopo un evento di ripristino di emergenza.
* diagramma di Hello illustra hello SAP NetWeaver ASCS e il livello di server dell'applicazione replicata da Azure Site Recovery.

![Scenario di replica](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Esecuzione di un failover di test
Seguire [questa Guida](azure-to-azure-walkthrough-test-failover.md) toodo un failover di test.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di servizi di ripristino.
2.  Fare clic sul piano di ripristino hello creato per le applicazioni SAP (s).
3.  Fare clic su 'Failover di test'.
4.  Selezionare un punto di ripristino e il processo di failover di test di rete virtuale di Azure toostart hello.
5.  Una volta ambiente secondario hello è attivo, è possibile eseguire le convalide.
6.  Dopo aver complete le convalide hello, fare clic su 'Failover di test di pulizia' e hello tooclean ambiente.

## <a name="doing-a-failover"></a>Esecuzione di un failover
Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di servizi di ripristino.
2.  Fare clic sul piano di ripristino hello creato per applicazioni SAP.
3.  Fare clic su 'Failover'.
4.  Seleziona processo di failover hello toostart punto di ripristino.

## <a name="next-steps"></a>Passaggi successivi
Leggere altre informazioni sulla creazione di una soluzione di ripristino di emergenza per le distribuzioni SAP NetWeaver con Azure Site Recovery in [questo white paper](http://aka.ms/asr-sap). white paper Hello inoltre vengono illustrati i consigli per diverse architetture SAP, Elenca i tipi di macchine Virtuali e applicazioni supportate per SAP in Azure e vengono descritti i piani di test possibili per la soluzione di ripristino di emergenza.

Leggere altre informazioni sulla [replica di altri carichi di lavoro](site-recovery-workload.md) con Site Recovery.
