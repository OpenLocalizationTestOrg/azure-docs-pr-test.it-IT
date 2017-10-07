---
title: "un'applicazione di SharePoint a più livelli usando Azure Site Recovery aaaReplicate | Documenti Microsoft"
description: "Questo articolo viene descritto come tooreplicate un'applicazione di SharePoint a più livelli con funzionalità di Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Eseguire la replica di un'applicazione di SharePoint multilivello per il ripristino di emergenza con Azure Site Recovery

In questo articolo descrive in dettaglio come un'applicazione di SharePoint con tooprotect [Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Panoramica

Microsoft SharePoint è una potente applicazione che può aiutare un gruppo o un reparto a organizzare e condividere informazioni collaborando. SharePoint offre portali Intranet, gestione di documenti e file, collaborazione, social network, reti Extranet, siti Web, ricerca di livello aziendale e business intelligence. Include inoltre funzionalità di integrazione dei sistemi, integrazione dei processi e automazione dei flussi di lavoro. In genere, le organizzazioni viene considerano come una livello 1 applicazione riservata toodowntime e perdita di dati.

Oggi Microsoft SharePoint non include funzionalità di ripristino di emergenza predefinite. Indipendentemente dal tipo hello e la scala di una situazione di emergenza, ripristino prevede l'uso di hello di un centro dati di standby che è possibile ripristinare la farm hello. Standby data center sono necessari per gli scenari in cui i sistemi di archiviazione con ridondanza locali e backup ingestibile interruzione hello in hello data center principale.

Una soluzione di ripristino di emergenza valida deve consentire la modellazione di piani di ripristino intorno architetture di applicazioni complesse hello, ad esempio SharePoint. Deve inoltre essere hello possibilità tooadd personalizzato passaggi toohandle applicazione mapping tra i vari livelli e fornendo un failover con clic singolo con un RTO inferiore nell'evento hello un'emergenza.

In questo articolo descrive in dettaglio come un'applicazione di SharePoint con tooprotect [Azure Site Recovery](site-recovery-overview.md). In questo articolo verrà illustrate le procedure consigliate per la replica di un tooAzure di applicazione di SharePoint a tre livelli, come è possibile eseguire un'analisi di ripristino di emergenza e come è possibile tooAzure applicazione hello di failover.

È possibile controllare hello seguito video sul ripristino di un tooAzure di applicazione di livello più.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di che aver compreso l'esempio hello:

1. [La replica tooAzure una macchina virtuale](site-recovery-vmware-to-azure.md)
2. Come troppo[progettare una rete di ripristino](site-recovery-network-design.md)
3. [Esegue un tooAzure di failover di test](site-recovery-test-failover-to-azure.md)
4. [Eseguire un failover tooAzure](site-recovery-failover.md)
5. Come troppo[replicare un controller di dominio](site-recovery-active-directory.md)
6. Come troppo[la replica di SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Architettura di SharePoint

SharePoint può essere distribuito in uno o più server usando topologie a livelli e ruoli di server tooimplement una progettazione di farm che soddisfi gli obiettivi e obiettivi specifici. Una tipica server farm di SharePoint con esigenze e dimensioni elevate che supporta molti utenti simultanei ed elementi di contenuto usa il raggruppamento dei servizi come parte della strategia di scalabilità. Questo approccio prevede l'esecuzione di servizi su server dedicati, raggruppare questi servizi e la scalabilità orizzontale server hello come gruppo. Hello topologia seguente viene illustrato il servizio di hello e server per una server farm di SharePoint a tre livelli di raggruppamento. Per indicazioni dettagliate sulle diverse topologie di SharePoint, vedere tooSharePoint documentazione e le architetture di riga del prodotto. Altre informazioni sulla distribuzione di SharePoint 2013 sono disponibili in [questo documento](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Modello di distribuzione 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Supporto di Site Recovery

Ai fini di questo articolo sono state usate macchine virtuali VMware con Windows Server 2012 R2 Enterprise. Sono stati usati SharePoint 2013 Enterprise Edition e SQL Server 2014 Enterprise Edition. Replica di Site Recovery è indipendente dall'applicazione, indicazioni hello forniti sono toohold previsto in negli scenari seguenti.

### <a name="source-and-target"></a>Origine e destinazione

**Scenario** | **sito secondario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sì | Sì
**VMware** | Sì | Sì
**Server fisico** | Sì | Sì

### <a name="sharepoint-versions"></a>Versioni di SharePoint
Hello seguenti versioni di SharePoint server è supportata.

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Operazioni tookeep presente

Se si utilizza un cluster basato su disco condiviso come qualsiasi livello dell'applicazione, non sarà possibile toouse in grado di Site Recovery replica tooreplicate tali macchine virtuali. È possibile utilizzare la replica nativa fornita da un'applicazione hello e quindi utilizzare un [piano di ripristino](site-recovery-create-recovery-plans.md) toofailover tutti i livelli.

## <a name="replicating-virtual-machines"></a>Replica di macchine virtuali

Seguire [questa Guida](site-recovery-vmware-to-azure.md) toostart hello tooAzure di macchina virtuale di replica.

* Una volta completata la replica di hello, assicurarsi di passare tooeach di macchina virtuale di ogni livello e selezionare stesso set di disponibilità in ' articolo replicato > Impostazioni > Proprietà > calcolo e rete ". Ad esempio, se il livello web dispone di 3 macchine virtuali, verificare hello tutte le macchine 3 virtuali sono configurate toobe parte della stesso set di disponibilità in Azure.

    ![Impostazione del set di disponibilità](./media/site-recovery-sharepoint/select-av-set.png)

* Per ulteriori informazioni sulla protezione di Active Directory e DNS, fare riferimento troppo[proteggere Active Directory e DNS](site-recovery-active-directory.md) documento.

* Per ulteriori informazioni sulla protezione a livello di database in esecuzione in SQL server, vedere troppo[proteggere SQL Server](site-recovery-active-directory.md) documento.

## <a name="networking-configuration"></a>Configurazione delle impostazioni di rete

### <a name="network-properties"></a>Proprietà di rete

* Per App hello e livello Web le macchine virtuali, configurare le impostazioni di rete nel portale di Azure in modo che le macchine virtuali hello ottenere toohello collegato corretto ripristino di emergenza rete dopo il failover.

    ![Selezione della rete](./media/site-recovery-sharepoint/select-network.png)


* Se si utilizza un indirizzo IP statico, quindi specificare hello IP che si desidera hello tootake macchina virtuale in hello **indirizzo IP di destinazione** campo

    ![Impostazione dell'IP statico](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS e routing del traffico

Per i siti per internet [creare un profilo di gestione traffico di tipo 'Priority'](../traffic-manager/traffic-manager-create-profile.md) in hello sottoscrizione di Azure. E quindi configurare il DNS e gestione traffico il profilo nel seguente modo hello.


| **Where** | **Origine** | **Destinazione**|
| --- | --- | --- |
| DNS pubblico | DNS pubblico per siti di SharePoint <br/><br/> Esempio: sharepoint.contoso.com | Gestione traffico <br/><br/> contososharepoint.trafficmanager.net |
| DNS locale | sharepointonprem.contoso.com | Indirizzo IP pubblico nella farm locale hello |


Nel profilo di gestione traffico, hello [creare hello endpoint primario e di ripristino](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Utilizzare l'endpoint esterno hello per endpoint locale e l'indirizzo IP pubblico per l'endpoint di Azure. Verificare che la priorità hello sia impostata endpoint locale tooon più elevata.

Host di una pagina di prova su una porta specifica (ad esempio 800) nel livello web di SharePoint hello affinché tooautomatically Traffic Manager di rilevare disponibilità post failover. Questa è una soluzione alternativa per i casi in cui non è possibile abilitare l'autenticazione anonima in uno dei siti di SharePoint.

[Configurare il profilo di gestione traffico hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md) con hello sotto le impostazioni.

* Metodo di routing: "Priorità"
* DNS ora toolive (TTL) - 30 ' secondi'
* Impostazioni di monitoraggio degli endpoint: se l'autenticazione anonima può essere abilitata, è possibile fornire l'endpoint di un sito Web specifico. In alternativa, è possibile usare una pagina di test su una porta specifica, ad esempio la porta 800.

## <a name="creating-a-recovery-plan"></a>Creazione di un piano di ripristino

Un piano di ripristino consente di sequenziazione failover hello di vari livelli di un'applicazione multilivello, di conseguenza, mantenendo la coerenza delle applicazioni. Seguire hello passaggi seguenti durante la creazione di un piano di ripristino per un'applicazione web a più livelli. [Altre informazioni sulla creazione di un piano di ripristino](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Aggiunta di gruppi toofailover macchine virtuali

1. Creare un piano di ripristino da hello aggiunta App e il livello Web le macchine virtuali.
2. Fare clic su 'Personalizza' toogroup hello macchine virtuali. Per impostazione predefinita, tutte le VM fanno parte di "Gruppo 1".

    ![Personalizzazione del piano di ripristino](./media/site-recovery-sharepoint/rp-groups.png)

3. Creare un altro gruppo (gruppo 2) e spostare il livello Web hello macchine virtuali nel nuovo gruppo di hello. Le VM di livello app devono fare parte di "Gruppo 1", mentre le VM di livello Web devono fare parte di "Gruppo 2". Si tratta di tooensure che hello macchine virtuali di livello avviano prima seguita dalle macchine virtuali di livello Web App.


### <a name="adding-scripts-toohello-recovery-plan"></a>Aggiunta di script toohello piano di ripristino

È possibile distribuire script di Azure Site Recovery hello più comunemente usato nell'account di automazione pulsante hello 'Distribuire tooAzure' riportata di seguito. Quando si utilizza uno script pubblicato, attenersi alle linee guida hello nello script hello.

[![Distribuire tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Aggiungere un script di pre-azione too'Group 1' toofailover gruppo di disponibilità SQL. Utilizzare lo script 'SQL ripristino automatico di sistema-FailoverAG' hello pubblicato negli script di esempio hello. Assicurarsi di seguire indicazioni hello nello script hello e apportare modifiche hello necessario nello script hello in modo appropriato.

    ![Aggiunta dello script per il gruppo di disponibilità - Passaggio 1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Aggiunta dello script per il gruppo di disponibilità - Passaggio 2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Aggiungere un tooattach script azione di post di un servizio di bilanciamento del carico hello failover le macchine virtuali del livello Web (gruppo 2). Utilizzare lo script 'Ripristino automatico di sistema-AddSingleLoadBalancer' hello pubblicato negli script di esempio hello. Assicurarsi di seguire indicazioni hello nello script hello e apportare modifiche hello necessario nello script hello in modo appropriato.

    ![Aggiunta dello script per il bilanciamento del carico - Passaggio 1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Aggiunta dello script per il bilanciamento del carico - Passaggio 2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Aggiungere una passaggio manuale tooupdate hello DNS record toopoint toohello nuova farm in Azure.

    * Per i siti con connessione Internet, non è necessario alcun aggiornamento dei record DNS dopo il failover. Seguire i passaggi di hello descritti in tooconfigure di sezione 'Informazioni aggiuntive sulla rete' hello Traffic Manager. Se hello profilo di gestione traffico è stato impostato come descritto nella sezione precedente di hello, aggiungere una porta di script tooopen fittizio (800 nell'esempio hello) in hello macchina virtuale di Azure.

    * Per siti Web interni, aggiungere l'IP del servizio di bilanciamento carico di un passaggio manuale tooupdate hello DNS record toopoint toohello nuova Web livello della macchina virtuale.

4. Aggiungere un'applicazione di ricerca toorestore passaggio manuale da un backup oppure avviare un nuovo servizio di ricerca.

5. Per il ripristino dell'applicazione del servizio di ricerca da un backup, seguire i passaggi seguenti.

    * Questo metodo presuppone che un backup di hello applicazione di servizio di ricerca è stato eseguito prima dell'evento irreversibile hello e tale backup hello è disponibile nel sito di ripristino di emergenza hello.
    * Può essere ottenuta facilmente pianificando backup hello (ad esempio, una volta al giorno) e usando un backup di copia procedure tooplace hello nel sito di ripristino di emergenza hello. Le procedure di copia possono includere programmi basati su script come AzCopy (Azure Copy) o la configurazione di DFSR (Distributed File Services Replication).
    * Ora che hello SharePoint farm è in esecuzione, passare hello Amministrazione centrale, 'Backup e ripristino' e selezionare il ripristino. ripristino Hello interroga il percorso di backup hello specificato (valore hello tooupdate potrebbe essere necessario). Selezionare il backup di applicazione di servizio di ricerca hello toorestore desiderato.
    * La ricerca viene ripristinata. Tenere presente che hello ripristino prevede toofind hello stessa topologia (stesso numero di server) e le stesse unità disco rigido lettere assegnate toothose server. Per altre informazioni, vedere il documento [Ripristinare le applicazioni del servizio di ricerca in SharePoint 2013](https://technet.microsoft.com/library/ee748654.aspx).


6. Per avviare il sistema con una nuova applicazione del servizio di ricerca, seguire i passaggi seguenti.

    * Questo metodo presuppone che nel sito di ripristino di emergenza hello è disponibile un backup del database "Di amministrazione della ricerca" hello.
    * Poiché hello altri database di applicazione di servizio di ricerca non vengono replicati, è necessario che toobe creato nuovamente. toodo consente pertanto di passare tooCentral amministrazione e di eliminare hello applicazione di servizio di ricerca. In tutti i server cui hello host indice di ricerca, eliminare i file di indice hello.
    * Ricreare hello applicazione di servizio di ricerca e si ricrea database hello. È consigliabile toohave uno script preparato che consente di ricreare questa applicazione del servizio perché non è possibile tooperform tutte le azioni tramite hello GUI. Posizione dell'indice unità hello e configurazione della topologia di ricerca hello sono, ad esempio, possibile solo tramite i cmdlet PowerShell di SharePoint. Utilizzare il cmdlet di Windows PowerShell hello SPEnterpriseSearchServiceApplication di ripristino e specificare hello soggetti a log Shipping e replica di database di amministrazione della ricerca, Search_Service__DB. Questo cmdlet consente la configurazione della ricerca hello, schema, proprietà gestite, regole e le origini e crea un set predefinito di hello altri componenti.
    * Dopo l'applicazione di servizio di ricerca sia hello creare di nuovo, è necessario avviare una ricerca per indicizzazione completa per ogni hello toorestore di origine di contenuto servizio di ricerca. Alcuni dati analitica dalla farm locale hello, ad esempio suggerimenti di ricerca andranno persi.

7. Una volta completati tutti i passaggi di hello, salvare il piano di ripristino hello e piano di ripristino finale hello avrà un aspetto simile riportato di seguito.

    ![Piano di ripristino salvato](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Esecuzione di un failover di test
Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali del servizio di ripristino.
2.  Fare clic sul piano di ripristino hello creato per l'applicazione di SharePoint.
3.  Fare clic su 'Failover di test'.
4.  Selezionare un punto di ripristino e il processo di failover di test di rete virtuale di Azure toostart hello.
5.  Una volta ambiente secondario hello è attivo, è possibile eseguire le convalide.
6.  Dopo aver complete le convalide hello, è possibile fare clic su 'Failover di test di pulizia' nel piano di ripristino hello e ambiente di failover di test hello verrà eliminate.

Per informazioni aggiuntive sull'esecuzione di test del failover per Active Directory e DNS, fare riferimento troppo[Test considerazioni sul failover per Active Directory e DNS](site-recovery-active-directory.md#test-failover-considerations) documento.

Per informazioni aggiuntive sull'esecuzione di test del failover di SQL nei gruppi di disponibilità, fare riferimento troppo[esegue Test del failover per SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) documento.

## <a name="doing-a-failover"></a>Esecuzione di un failover
Seguire [queste linee guida](site-recovery-failover.md) per eseguire un failover.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali di servizi di ripristino.
2.  Fare clic sul piano di ripristino hello creato per l'applicazione di SharePoint.
3.  Fare clic su 'Failover'.
4.  Seleziona processo di failover hello toostart punto di ripristino.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla [replica di altre applicazioni](site-recovery-workload.md) con Site Recovery.
