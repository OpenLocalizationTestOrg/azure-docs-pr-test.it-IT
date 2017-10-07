---
title: "aaaReplicate un server IIS a più livelli in base a un'applicazione web con Azure Site Recovery | Documenti Microsoft"
description: In questo articolo viene descritto come tooreplicate IIS web farm le macchine virtuali usando Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Eseguire la replica di un'applicazione Web multilivello basata su IIS usando Azure Site Recovery

## <a name="overview"></a>Panoramica


Software dell'applicazione è il motore di hello di produttività aziendale in un'organizzazione. Le diverse applicazioni Web possono essere usate per scopi diversi in un'organizzazione. Alcune di queste, come le applicazioni per l'elaborazione delle retribuzioni, le applicazioni finanziarie e i siti Web rivolti ai clienti possono essere fondamentali. È importante per hello organizzazione toohave i backup e in esecuzione in perdita tooprevent tutti gli orari di produttività e più importante evitare qualsiasi immagine di marchio toohello di danni di organizzazione hello.

Applicazioni web critici vengono in genere impostate come applicazioni a più livelli con web hello, database e dell'applicazione in livelli diversi. Oltre a essere disseminate in vari livelli, hello possono anche essere utilizzati dalle applicazioni più server in ogni livello tooload hello bilanciare. Mapping di hello tra i vari livelli e nel server web hello, inoltre, possono essere basati su indirizzi IP statici. In caso di failover, alcuni di questi mapping sarà necessario toobe aggiornato, in particolare, se si dispone di più siti Web configurato nel server web hello. In caso di applicazioni web tramite SSL, le associazioni certificato saranno necessario toobe aggiornato.

Metodi di ripristino in base a non replica tradizionale implicano il backup di file di configurazione, le impostazioni del Registro di sistema, associazioni, i componenti personalizzati (COM o .NET), contenuto e anche i certificati e recupero file hello attraverso una serie di passaggi manuali. Queste tecniche sono chiaramente complesse, soggette a errori e non scalabili. È, ad esempio, possibile facilmente per tooforget il backup dei certificati e rimasta con nessuna scelta ma toobuy nuovi certificati per server hello dopo il failover.

Una soluzione di ripristino di emergenza valido, deve consentire di modellazione dei piani di ripristino intorno hello sopra architetture di applicazioni complesse e dispongano di hello possibilità tooadd personalizzato passaggi toohandle applicazione mapping tra i vari livelli fornendo un con clic singolo che cattura soluzione nell'evento hello un'emergenza iniziali tooa inferiore RTO.


Questo articolo viene descritto come tooprotect IIS basato su applicazione web mediante un [Azure Site Recovery](site-recovery-overview.md). In questo articolo verrà illustrate le procedure consigliate per la replica di una a tre livelli basati su IIS tooAzure applicazione web, come è possibile eseguire un'analisi di ripristino di emergenza e come è possibile tooAzure applicazione hello di failover.


## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di che aver compreso l'esempio hello:

1. [La replica tooAzure una macchina virtuale](site-recovery-vmware-to-azure.md)
1. Come troppo[progettare una rete di ripristino](site-recovery-network-design.md)
1. [Esegue un tooAzure di failover di test](./site-recovery-test-failover-to-azure.md)
1. [Eseguire un failover tooAzure](site-recovery-failover.md)
1. Come troppo[replicare un controller di dominio](site-recovery-active-directory.md)
1. Come troppo[la replica di SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modelli di distribuzione
Un'applicazione web IIS basato in genere si basa su uno di hello seguenti modelli di distribuzione:

**Modello di distribuzione 1 ** Web farm basata su IIS con Application Request Routing (ARR), server IIS e Microsoft SQL Server.

![Modello di distribuzione](./media/site-recovery-iis/deployment-pattern1.png)

**Modello di distribuzione 2** Web farm basata su IIS con Application Request Routing (ARR), server IIS, server applicazioni e Microsoft SQL Server.


![Modello di distribuzione](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Supporto di Site Recovery

Sono stati utilizzati a scopo di hello di creazione di questo articolo le macchine virtuali VMware con Server IIS versione 7.5 in Windows Server 2012 R2 Enterprise. Replica di ripristino del sito è indipendente dall'applicazione, indicazioni di hello forniti sono toohold previsto negli scenari seguenti e per diverse versioni di IIS.

### <a name="source-and-target"></a>Origine e destinazione

**Scenario** | **sito secondario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sì | Sì
**VMware** | Sì | Sì
**Server fisico** | No | Sì

## <a name="replicate-virtual-machines"></a>Replicare le macchine virtuali

Seguire [questa Guida](site-recovery-vmware-to-azure.md) toostart tooAzure tutti hello IIS web farm macchine virtuali di replica.

Se si utilizza un indirizzo IP statico, specificare hello IP che si desidera hello tootake macchina virtuale in hello [ **indirizzo IP di destinazione** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) impostazione nelle impostazioni di calcolo e di rete.

![IP di destinazione](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Creazione di un piano di ripristino

Un piano di ripristino consente di sequenziazione failover hello di vari livelli di un'applicazione multilivello, di conseguenza, mantenendo la coerenza delle applicazioni. Seguire hello passaggi seguenti durante la creazione di un piano di ripristino per un'applicazione web a più livelli.  [Altre informazioni sulla creazione di un piano di ripristino](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Aggiunta di gruppi toofailover macchine virtuali
Una tipica applicazione web IIS a più livelli sarà costituito da un livello di database con le macchine virtuali SQL, livello web hello costituita da un server IIS e un livello di applicazione. Aggiungere tutti questi gruppo toodifferent macchine virtuali in base a livello di seguito. [Altre informazioni sulla personalizzazione dei piani di ripristino](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Creare un piano di ripristino. Aggiungere macchine virtuali del livello database hello in gruppo 1 tooensure che sono ultimo arresto e portato per primo.

1. Aggiungere macchine virtuali del livello applicazione hello gruppo 2, in modo che essi vengono attivati dopo aver portato il livello di database hello.

1. Aggiungere macchine virtuali del livello web hello in gruppo 3 in modo che essi vengono attivati dopo aver portato il livello di applicazione hello.

1. Aggiungere bilanciare il carico di macchine virtuali nel gruppo 4 in modo che essi vengono attivati dopo che è stata portata livello web hello.


### <a name="adding-scripts-toohello-recovery-plan"></a>Aggiunta di script toohello piano di ripristino
Potrebbe essere necessario toodo alcune operazioni su macchine virtuali di Azure post failover o Test failover toomake IIS web farm funzione hello correttamente. È possibile automatizzare operazione di failover hello post come aggiornamento voce DNS, la modifica di associazione del sito, modificare nella stringa di connessione mediante l'aggiunta di script corrispondenti nel piano di ripristino hello come indicato di seguito. [Altre informazioni sull'aggiunta di script al piano di ripristino](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>Aggiornamento del DNS
Se hello DNS è configurato per l'aggiornamento dinamico DNS, quindi le macchine virtuali, in genere, aggiornare hello DNS con hello nuovo indirizzo IP quando vengono avviati. Se si desidera tooadd tooupdate un passaggio esplicita DNS con hello nuovi indirizzi IP delle macchine virtuali hello quindi aggiungere questo [script tooupdate IP nel DNS](https://aka.ms/asr-dns-update) come un'azione post su gruppi del piano di ripristino.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Stringa di connessione nel file web.config di un'applicazione
stringa di connessione Hello specifica database hello hello sito web comunica con.

Se la stringa di connessione hello viene assegnato il nome di hello della macchina virtuale di hello database, non altri passaggi saranno necessari post failover e applicazione hello sarà in grado di comunicare tooautomatically toohello DB. Inoltre, se l'indirizzo IP hello per la macchina virtuale di hello database viene mantenuto, non sarà necessaria una stringa di connessione tooupdate hello. Se la stringa di connessione hello fa riferimento toohello macchina virtuale di database utilizzando un indirizzo IP, sarà necessario failover post toobe aggiornato. Ad esempio, Hello di sotto di stringa di connessione punti toohello DB con IP 127.0.1.2

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

È possibile aggiornare la stringa di connessione hello nel livello web aggiungendo [script di aggiornamento di connessione IIS](https://aka.ms/asr-update-webtier-script-classic) dopo 3 gruppo nel piano di ripristino hello.

#### <a name="site-bindings-for-hello-application"></a>Associazioni di sito per un'applicazione hello
Ogni sito consiste in informazioni che include il tipo di hello di associazione, l'indirizzo IP di hello sul quale hello server IIS è in ascolto di richieste toohello per sito hello, numero di porta hello e hello host per il sito hello. In fase di hello di un failover, queste associazioni potrebbe essere necessario toobe aggiornata se è presente una modifica dell'indirizzo IP di hello associata.

> [!NOTE]
>
> Se è stato contrassegnato come 'all unassigned' per il binding del sito hello come esempio hello seguente, non occorre tooupdate questo failover post di associazione. Inoltre, se l'indirizzo IP hello associata a un sito non viene modificato post-failover, binding del sito hello necessario non aggiornate (memorizzazione dell'indirizzo IP hello dipende dall'architettura di rete hello e subnet assegnato toohello siti primario e di ripristino e pertanto potrebbero essere o non possono essere fattibile per l'organizzazione.)

![Binding SSL](./media/site-recovery-iis/sslbinding.png)

Se è stato associato l'indirizzo IP hello con un sito, è necessario tooupdate tutte le associazioni del sito con il nuovo indirizzo IP di hello. È possibile aggiungere [script di aggiornamento di livello Web IIS](https://aka.ms/asr-web-tier-update-runbook-classic) dopo il gruppo 3 nei binding del sito di ripristino piano toochange hello.


#### <a name="update-load-balancer-ip-address"></a>Aggiornare l'indirizzo IP del servizio di bilanciamento del carico
Se si dispone di Application Request Routing macchina virtuale, aggiungere [script failover ARR IIS](https://aka.ms/asr-iis-arrtier-failover-script-classic) dopo l'indirizzo IP di hello tooupdate gruppo 4.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>associazione certificato SSL di Hello per una connessione https
Siti Web può avere un certificato SSL associato che consente di garantire una comunicazione sicura tra i server Web hello e browser dell'utente hello. Se il sito Web di hello disponga di una connessione https e un indirizzo IP di toohello associazione di sito associato https del server IIS hello con un'associazione certificato SSL, una nuova associazione di sito sarà necessario toobe aggiunto per cert hello con hello IP della macchina virtuale IIS hello post-failover.

certificato SSL Hello può essere eseguito in base-

) nome di dominio completo hello del sito Web di hello<br>
b) nome hello del server di hello<br>
c) un certificato con caratteri jolly per il nome di dominio hello<br>
d) è un indirizzo IP: se certificato SSL hello viene eseguita in IP hello del server IIS hello, toobe esigenze di un'altra SSL cert eseguita sull'indirizzo IP hello di hello server IIS in Azure site hello e un'associazione SSL aggiuntiva per il certificato sarà necessario toobe creato. Di conseguenza, è consigliabile toonot utilizzare un certificato SSL emesso in base IP. Si tratta di un'opzione meno usata e verrà presto deprecata in base alle nuove modifiche di CA/Browser Forum.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Aggiornamento hello dipendenza tra web hello e livello di applicazione hello
Se si dispone di una dipendenza specifico dell'applicazione in base all'indirizzo IP hello delle macchine virtuali hello, è necessario tooupdate questa dipendenza post di failover.

## <a name="doing-a-test-failover"></a>Esecuzione di un failover di test
Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali del servizio di ripristino.
1.  Fare clic sul piano di ripristino hello creato per una web farm IIS.
1.  Fare clic su 'Failover di test'.
1.  Selezionare un punto di ripristino e il processo di failover di test di rete virtuale di Azure toostart hello.
1.  Una volta ambiente secondario hello è attivo, è possibile eseguire le convalide.
1.  Dopo aver complete le convalide hello, è possibile selezionare 'Convalide completare' e ambiente di failover di test hello verrà pulita.

## <a name="doing-a-failover"></a>Esecuzione di un failover
Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.

1.  Passare tooAzure portale e selezionare l'insieme di credenziali del servizio di ripristino.
1.  Fare clic sul piano di ripristino hello creato per una web farm IIS.
1.  Fare clic su 'Failover'.
1.  Seleziona processo di failover hello toostart punto di ripristino.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla [replica di altre applicazioni](site-recovery-workload.md) con Site Recovery.
