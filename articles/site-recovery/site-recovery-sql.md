---
title: le applicazioni con SQL Server e Azure Site Recovery aaaReplicate | Documenti Microsoft
description: "Questo articolo viene descritto come tooreplicate SQL Server con Azure Site Recovery per le funzionalità di emergenza di SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Proteggere SQL Server con il ripristino di emergenza di SQL Server e Azure Site Recovery

In questo articolo viene descritto come tooprotect hello Server SQL back-end di un'applicazione utilizzando una combinazione di continuità aziendale di SQL Server e tecnologie di ripristino di emergenza, e [Azure Site Recovery](site-recovery-overview.md).

Prima di iniziare, acquisire familiarità con le funzionalità di ripristino di emergenza di SQL Server, come il clustering di failover, i gruppi di disponibilità AlwaysOn, il mirroring del database e il log shipping.


## <a name="sql-server-deployments"></a>Distribuzioni di SQL Server

Molti carichi di lavoro utilizzare SQL Server come base, e può essere integrato con applicazioni quali SAP, i servizi dati tooimplement, Dynamics e SharePoint.  È possibile distribuire SQL Server in diversi modi.

* **SQL Server autonomo**: SQL Server e tutti i database sono ospitati in un singolo computer (fisico o una macchina virtuale). Se è virtualizzato, il clustering dell'host viene usato per la disponibilità elevata. La disponibilità elevata a livello di guest non viene implementata.
* **Istanze di clustering di failover di SQL Server (AlwaysOn)**: due o più nodi che eseguono istanze di SQL Server con dischi condivisi vengono configurati in un cluster di failover di Windows. Se un nodo è attivo, il cluster hello il failover SQL Server tooanother istanza. Il programma di installazione è in genere utilizzate tooimplement la disponibilità elevata in un sito primario. Questa distribuzione non protegge da un'interruzione nel livello di archiviazione condivisa hello o un errore. Un disco condiviso può essere implementato con iSCSI, Fibre Channel o VHDX condiviso.
* **Gruppi di disponibilità SQL AlwaysOn**: due o più nodi vengono configurati in un cluster non condiviso con i database SQL Server configurati in un gruppo di disponibilità con replica sincrona e failover automatico.

 In questo articolo si avvale di hello native tecnologie di ripristino di emergenza SQL per il ripristino del sito remoto tooa di database seguenti:

* SQL gruppi di disponibilità AlwaysOn, tooprovide per il ripristino di emergenza per SQL Server 2012 o 2014 Enterprise Edition.
* Mirroring del database SQL in modalità protezione elevata, per SQL Server Standard Edition (qualsiasi versione) o SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Supporto di Site Recovery

### <a name="supported-scenarios"></a>Scenari supportati
Site Recovery può proteggere SQL Server, come riepilogato nella tabella hello.

**Scenario** | **sito secondario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sì | Sì
**VMware** | Sì | Sì
**Server fisico** | Sì | Sì

### <a name="supported-sql-server-versions"></a>Versioni di SQL Server supportate
Queste versioni di SQL Server sono supportate, per gli scenari di hello è supportato:

* SQL Server 2016 Enterprise e Standard
* SQL Server 2014 Enterprise e Standard
* SQL Server 2012 Enterprise e Standard
* SQL Server 2008 R2 Enterprise e Standard

### <a name="supported-sql-server-integration"></a>Supporto dell'integrazione con SQL Server

Il ripristino del sito può essere integrato con le tecnologie di SQL Server BCDR native riepilogate nella tabella hello tooprovide una soluzione di ripristino di emergenza.

**Funzionalità** | **Dettagli** | **SQL Server** |
--- | --- | ---
**Gruppo di disponibilità AlwaysOn** | Ognuna delle istanze autonome multiple di SQL Server viene eseguita in un cluster di failover con più nodi.<br/><br/>I database possono essere raggruppati in gruppi di failover che possono essere copiati (con mirroring) in istanze di SQL Server in modo che non sia necessaria alcuna archiviazione condivisa.<br/><br/>Fornisce il ripristino di emergenza tra un sito primario e uno o più siti secondari. Due nodi possono essere configurati in un cluster non condiviso con i database di SQL Server configurati in un gruppo di disponibilità con replica sincrona e failover automatico. | SQL Server 2014 e 2012 Enterprise
**Clustering di failover (istanza del cluster di failover AlwaysOn)** | SQL Server usa il clustering di failover di Windows per l'elevata disponibilità dei carichi di lavoro SQL Server locali.<br/><br/>I nodi che eseguono le istanze di SQL Server con dischi condivisi sono configurati in un cluster di failover. Caso un'istanza cluster hello failover toodifferent uno.<br/><br/>cluster Hello non proteggono da errori o interruzioni del servizio nel servizio di archiviazione condivisa. disco condiviso Hello può essere implementato con iSCSI, fibre channel, oppure Vhdx condiviso. | Edizioni SQL Server Enterprise<br/><br/>SQL Server Standard edition (solo nodi tootwo limitato)
**Mirroring del database (modalità di protezione elevata)** | Consente di proteggere una copia del database singola tooa singolo secondario. Disponibile nelle modalità di replica a protezione elevata (sincrona) e a prestazione elevata (asincrona). Non richiede un cluster di failover. | SQL Server 2008 R2<br/><br/>Tutte le edizioni di SQL Server Enterprise
**SQL Server autonomo** | Hello SQL Server e database sono ospitati in un server singolo (fisico o virtuale). Clustering degli host viene utilizzato per la disponibilità elevata se virtual server hello. Nessuna disponibilità elevata a livello di guest. | Edizione Enterprise o Standard

## <a name="deployment-recommendations"></a>Indicazioni di distribuzione

Nella tabella seguente vengono riepilogate le indicazioni per l'integrazione delle tecnologie di continuità aziendale e ripristino di emergenza (BCDR) di SQL Server con Site Recovery.

| **Versione** | **Edizione** | **Distribuzione** | **Locale tooon locale** | **TooAzure locale** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 o 2012 |Enterprise |Istanza del cluster di failover |Gruppi di disponibilità AlwaysOn |Gruppi di disponibilità AlwaysOn |
|| Enterprise |Gruppo di disponibilità AlwaysOn per la disponibilità elevata |Gruppi di disponibilità AlwaysOn |Gruppi di disponibilità AlwaysOn | |
|| Standard |Istanza del cluster di failover (FCI) |Replica di Site Recovery con mirror locale |Replica di Site Recovery con mirror locale | |
|| Enterprise o Standard |Autonoma |Replica di Site Recovery |Replica di Site Recovery | |
| SQL Server 2008 R2 o 2008 |Enterprise o Standard |Istanza del cluster di failover (FCI) |Replica di Site Recovery con mirror locale |Replica di Site Recovery con mirror locale |
|| Enterprise o Standard |Autonoma |Replica di Site Recovery |Replica di Site Recovery | |
| SQL Server (qualsiasi versione) |Enterprise o Standard |Istanza del cluster di failover: applicazione DTC |Replica di Site Recovery |Non supportato |

## <a name="deployment-prerequisites"></a>Prerequisiti di distribuzione

* Distribuzione di SQL Server locale che esegue una versione supportata di SQL Server. In genere è necessario anche Active Directory per il server SQL.
* requisiti di Hello per hello scenario si desidera toodeploy. Ulteriori informazioni sui requisiti di supporto per [replica tooAzure](site-recovery-support-matrix-to-azure.md) e [locale](site-recovery-support-matrix.md), e [prerequisiti di distribuzione](site-recovery-prereq.md).
* tooset il ripristino in Azure, hello esecuzione [valutazione della macchina virtuale Azure](http://www.microsoft.com/download/details.aspx?id=40898) strumento nelle macchine virtuali di SQL Server, toomake che sono sia compatibile con Azure e il ripristino del sito.

## <a name="set-up-active-directory"></a>Configurare Active Directory

Configurare Active Directory, nel sito di ripristino secondario, hello toorun di SQL Server in modo corretto.

* **Aziende di piccole dimensioni**, con un numero limitato di applicazioni e un singolo controller di dominio per il sito locale hello, se si desidera toofail sulla hello dell'intero sito, è consigliabile usare Site Recovery replica tooreplicate hello controller di dominio Data Center secondario toohello o tooAzure.
* **Enterprise toolarge Medium**: se si dispone di un numero elevato di applicazioni, una foresta di Active Directory, e si desidera toofail base al carico di lavoro o all'applicazione, è consigliabile impostare un controller di dominio aggiuntivo in Data Center secondario hello o in Azure. Se si usa Always On disponibilità gruppi toorecover tooa del sito remoto, è consigliabile che impostare un altro controller di dominio aggiuntivo nel sito secondario hello o in Azure, toouse hello recuperato istanza di SQL Server.

istruzioni di Hello in questo articolo presuppongono che un controller di dominio è disponibile nel percorso secondario hello. [Altre informazioni](site-recovery-active-directory.md) sulla protezione di Active Directory con Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Integrazione con SQL Server AlwaysOn per la replica tooAzure

Ecco cosa occorre toodo:

1. Importare gli script nell'account di Automazione di Azure. Questo file contiene hello script toofailover gruppo di disponibilità SQL in un [macchina virtuale di gestione risorse](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) e un [macchina virtuale classica](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Distribuire tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Aggiungere ASR-SQL-FailoverAG come azione pre del primo gruppo di hello hello del piano di ripristino.

1. Seguire le istruzioni di hello disponibili in hello script toocreate un nome di hello tooprovide variabile di automazione hello dei gruppi di disponibilità.

### <a name="steps-toodo-a-test-failover"></a>Passaggi toodo un failover di test

SQL AlwaysOn non supporta il failover di test in modo nativo. È pertanto consigliabile seguente hello:

1. Impostare [Azure Backup](../backup/backup-azure-vms.md) nella macchina virtuale hello che ospita una replica del gruppo di disponibilità hello in Azure.

1. Prima di attivare il failover di test hello del piano di ripristino, ripristinare macchina virtuale hello da backup hello creato nel passaggio precedente hello.

    ![Eseguire il ripristino da Backup di Azure ](./media/site-recovery-sql/restore-from-backup.png)

1. [Forzare un quorum](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) nella macchina virtuale hello ripristinato dal backup.

1. Aggiornare l'indirizzo IP di hello listener tooan IP disponibile in rete di failover di test hello.

    ![Aggiornare l'indirizzo IP del listener](./media/site-recovery-sql/update-listener-ip.png)

1. Portare online il listener.

    ![Portare online il listener](./media/site-recovery-sql/bring-listener-online.png)

1. Creare un servizio di bilanciamento del carico con un IP creati nel server front-end IP pool corrispondente tooeach listener gruppo di disponibilità e con la macchina virtuale SQL hello aggiunto nel pool back-end hello.

     ![Creazione del servizio di bilanciamento del carico - Pool di indirizzi front-end ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Creazione del servizio di bilanciamento del carico - Pool back-end ](./media/site-recovery-sql/create-load-balancer2.png)

1. Eseguire un failover di test hello del piano di ripristino.

### <a name="steps-toodo-a-failover"></a>Passaggi toodo un failover

Dopo aver aggiunto script hello nel piano di ripristino hello e piano di ripristino hello convalidato eseguendo un failover di test, è possibile eseguire failover hello del piano di ripristino.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Integrazione con SQL Server AlwaysOn per la replica tooa secondario nel sito locale

Se hello SQL Server utilizza i gruppi di disponibilità per la disponibilità elevata (o un'istanza FCI), è consigliabile utilizzare gruppi di disponibilità nel sito di ripristino hello anche. Si noti che questo si applica tooapps che non utilizzano transazioni distribuite.

1. [Configurare i database](https://msdn.microsoft.com/library/hh213078.aspx) in gruppi di disponibilità.
1. Creare una rete virtuale nel sito secondario hello.
1. Consente di impostare una connessione VPN da sito a sito tra la rete virtuale hello e sito primario di hello.
1. Creare una macchina virtuale nel sito di ripristino hello e installare SQL Server su di esso.
1. Estendere hello esistente Always On disponibilità gruppi toohello nuova VM SQL Server. Configurare l'istanza di SQL Server come una copia di replica asincrona.
1. Creare un listener del gruppo di disponibilità o aggiornamento hello esistente listener tooinclude hello replica asincrona virtual machine.
1. Assicurarsi che la farm di applicazione hello è impostata il utilizza hello listener. Se il programma di installazione utilizzando nome server di database hello, aggiornarlo listener hello toouse, pertanto non è necessario tooreconfigure dopo il failover hello.

Per le applicazioni che usano transazioni distribuite, è consigliabile distribuire Site Recovery con la [replica da sito a sito di VM VMware/server fisici](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Considerazioni sul piano di ripristino
1. Aggiungere questa libreria VMM toohello script di esempio, in siti primari e secondari hello.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Quando si crea un piano di ripristino per un'applicazione hello, aggiungere un pre-1 tooGroup tramite script passaggio dell'azione, che richiama hello script toofail sui gruppi di disponibilità.

## <a name="protect-a-standalone-sql-server"></a>Proteggere un'istanza di SQL Server autonoma

In questo scenario, è consigliabile utilizzare computer SQL Server di ripristino del sito replica tooprotect hello. la procedura esatta Hello variano se SQL Server è una macchina virtuale o un server fisico e se si desidera tooreplicate tooAzure o un database secondario locale del sito. Vedere l'articolo relativo agli [scenari di Site Recovery](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Proteggere un cluster SQL Server (Standard Edition/Windows Server 2008 R2)

Per un cluster che esegue SQL Server Standard edition o SQL Server 2008 R2, è consigliabile che utilizzare il ripristino del sito replica tooprotect SQL Server.

### <a name="on-premises-tooon-premises"></a>Tooon tra più sedi locali

* Se l'applicazione hello utilizza transazioni distribuite, è consigliabile distribuire [Site Recovery con replica SAN](site-recovery-vmm-san.md) per un ambiente Hyper-V, o [tooVMware server VMware/fisici](site-recovery-vmware-to-vmware.md) per un ambiente VMware.
* Per le applicazioni non DTC, utilizzare hello di sopra del cluster di approccio toorecover hello come server autonomo, mediante l'utilizzo di una database mirror di una protezione elevata locale.

### <a name="on-premises-tooazure"></a>TooAzure locale

Il ripristino del sito non fornisce guest quando si replicano tooAzure supporto dei cluster. Inoltre, SQL Server non fornisce una soluzione di ripristino di emergenza a costo contenuto per l'edizione Standard. In questo scenario, è consigliabile proteggere hello on-premise SQL Server cluster tooa computer SQL Server autonomo e ripristinarlo in Azure.

1. Configurare un'istanza di SQL Server autonomi aggiuntivi nel sito locale hello.
1. Configurare hello istanza tooserve come mirror di hello i database si desidera tooprotect. Configurare il mirroring in modalità protezione elevata.
1. Configurare il ripristino del sito nel sito locale hello, per ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) o [server macchine virtuali VMware/fisici)](site-recovery-vmware-to-azure-classic.md).
1. Utilizzare il ripristino del sito replica tooreplicate hello nuovo SQL Server istanza tooAzure. Poiché si tratta di una copia speculare protezione elevata, tale elemento verrà sincronizzato con cluster primario hello, ma sarà tooAzure replicati tramite replica di Site Recovery.


![Cluster standard](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Considerazioni sul failback

Per i cluster di SQL Server Standard, eseguire il failback dopo un failover non pianificato richiede un backup di SQL server e il ripristino, da hello mirror istanza toohello cluster originale, con i ripristino del saldo dei mirror hello.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni](site-recovery-components.md) sull'architettura di Site Recovery.
