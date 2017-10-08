---
title: "aaaSet la disponibilità elevata per le macchine virtuali di Azure Resource Manager | Documenti Microsoft"
description: "Questa esercitazione viene illustrato come raggruppare i toocreate un di disponibilità Always On con macchine virtuali di Azure in modalità Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Configurare manualmente un gruppo di disponibilità Always On nelle macchine virtuali di Azure tramite Resource Manager

Questa esercitazione viene illustrato come toocreate disponibilità di SQL Server gruppo che usa macchine virtuali di Azure Resource Manager. esercitazione di Hello Usa Azure pannelli tooconfigure un modello. È possibile esaminare le impostazioni predefinite di hello, digitare le impostazioni necessarie e aggiornare i pannelli hello nel portale di hello nel corso di questa esercitazione.

esercitazione completa Hello crea un gruppo di disponibilità di SQL Server in macchine virtuali Azure che includono hello seguenti elementi:

* Una rete virtuale con più subnet, inclusa una subnet front-end e una back-end
* Due controller di dominio che hanno un dominio di Active Directory
* Due macchine virtuali che eseguono SQL Server e sono distribuite toohello subnet di back-end e toohello aggiunti a un dominio di Active Directory
* Un cluster di failover di tre nodi con modello di quorum maggioranza dei nodi hello
* Un gruppo di disponibilità che ha due repliche di commit sincrono di un database di disponibilità

Hello nella figura seguente rappresenta una soluzione completa hello.

![Architettura di lab di test per gruppi di disponibilità in Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Tutte le risorse in questa soluzione appartengono tooa singolo gruppo di risorse.

Prima di iniziare questa esercitazione, verificare i seguenti hello:

* Si dispone già di un account Azure. In caso contrario, [iscriversi per ottenere un account di valutazione](http://azure.microsoft.com/pricing/free-trial/).
* Si conosce già la modalità toouse hello GUI tooprovision una macchina virtuale di SQL Server dalla raccolta di macchine virtuali hello. Per altre informazioni, vedere [Effettuare il provisioning di una macchina virtuale di SQL Server nel portale di Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Si ha già una conoscenza approfondita dei gruppi di disponibilità. Per altre informazioni, vedere [Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Se si è interessati all'uso di gruppi di disponibilità con SharePoint, vedere anche [Configurare gruppi di disponibilità AlwaysOn di SQL Server 2012 per SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

In questa esercitazione, usare hello Azure portale per:

* Scegliere il modello Always On di hello dal portale hello.
* Rivedere le impostazioni del modello hello e aggiornare alcune impostazioni di configurazione per l'ambiente.
* Monitorare Azure durante la creazione di tutto l'ambiente hello.
* Connettere il controller di dominio tooa, quindi tooa server che esegue SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Cluster di effettuare il provisioning hello dalla raccolta hello
Azure offre un'immagine della raccolta per l'intera soluzione hello. modello di hello toolocate:

1. Accedi toohello portale di Azure usando l'account.
2. Nel portale di Azure hello, fare clic su **+ nuovo** tooopen hello **New** blade.
3. In hello **New** pannello, cercare **AlwaysOn**.
   ![Individuare il modello AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Nei risultati della ricerca hello, individuare **Cluster di SQL Server AlwaysOn**.
   ![Modello AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. In **Selezionare un modello di distribuzione** scegliere **Resource Manager**.

### <a name="basics"></a>Nozioni di base
Fare clic su **nozioni di base** e configurare hello seguenti impostazioni:

* **Nome utente dell'amministratore** è un account utente che dispone delle autorizzazioni di amministratore di dominio ed è un membro del ruolo server predefinito sysadmin di SQL Server hello in entrambe le istanze di SQL Server. Per questa esercitazione, usare **DomainAdmin**.
* **Password** hello password per l'account amministratore di dominio hello. Usare una password complessa. Conferma password hello.
* **Sottoscrizione** sottoscrizione hello che Azure addebita distribuito toorun tutte le risorse per il gruppo di disponibilità hello. Se l'account ha più sottoscrizioni, è possibile specificare una sottoscrizione diversa.
* **Gruppo di risorse** nome hello hello gruppo toowhich appartengono tutte le risorse di Azure che vengono create da questo modello. Per questa esercitazione usare **SQL-HA-RG**. Per altre informazioni, vedere [Panoramica di Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Percorso** è hello regione di Azure in cui hello esercitazione consente di creare risorse hello. Scegliere un'area di Azure.

Hello screenshot che segue è un completato **nozioni di base** pannello:

![Nozioni di base](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Fare clic su **OK**.

### <a name="domain-and-network-settings"></a>Impostazioni di dominio e di rete
Questo modello di raccolta di Azure crea un dominio con controller di dominio. Crea inoltre una rete e due subnet. modello Hello non è possibile creare i server in una rete virtuale o un dominio esistente. passaggio successivo Hello Configura le impostazioni di rete e di dominio hello.

In hello **le impostazioni di rete e di dominio** pannello revisione hello valori predefiniti per le impostazioni di rete e di dominio hello:

* **Nome dominio radice della foresta** è il nome di dominio hello per dominio di Active Directory hello tale cluster hello host. Per l'esercitazione hello, utilizzare **contoso.com**.
* **Nome di rete virtuale** è il nome di rete hello per hello rete virtuale di Azure. Per l'esercitazione hello, utilizzare **autohaVNET**.
* **Nome di subnet di Controller di dominio** è il nome di hello di una parte della rete virtuale hello tale controller di dominio host hello. Usare **subnet-1**. Questa subnet usa il prefisso dell'indirizzo **10.0.0.0/24**.
* **Nome di subnet di SQL Server** hello nome di una parte della rete virtuale di hello che i server di hello host che eseguono SQL Server e file hello condividano di controllo. Usare **subnet-2**. Questa subnet usa il prefisso dell'indirizzo **10.0.1.0/26**.

toolearn sulle reti virtuali in Azure, vedere [Panoramica di rete virtuale](../../../virtual-network/virtual-networks-overview.md).  

Hello **le impostazioni di rete e di dominio** deve hello l'aspetto seguente schermata:

![Impostazioni di dominio e di rete](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Se necessario, questi valori possono essere modificati. Per questa esercitazione, è possibile utilizzare valori predefiniti di hello.

Rivedere le impostazioni di hello e quindi fare clic su **OK**.

### <a name="availability-group-settings"></a>Impostazioni gruppo di disponibilità
In **le impostazioni di gruppo di disponibilità**, revisione hello valori predefiniti per il gruppo di disponibilità hello e hello listener.

* **Nome del gruppo di disponibilità** hello risorsa cluster nome per il gruppo di disponibilità hello. Per questa esercitazione usare **Contoso-ag**.
* **Nome del listener del gruppo di disponibilità** viene utilizzato dal cluster hello e bilanciamento del carico interno hello. I client che si connettono tooSQL Server possono usare questa replica appropriata di toohello tooconnect nome del database hello. Per questa esercitazione usare **Contoso-listener**.
* **Porta del listener gruppo di disponibilità** specifica la porta TCP hello del listener di SQL Server hello. Per questa esercitazione, usare la porta predefinita hello, **1433**.

Se necessario, questi valori possono essere modificati. Per questa esercitazione, è possibile utilizzare valori predefiniti di hello.  

![Impostazioni gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Fare clic su **OK**.

### <a name="virtual-machine-size-storage-settings"></a>Impostazioni delle dimensioni della macchina virtuale e di archiviazione
In **dimensioni delle macchine Virtuali, le impostazioni di archiviazione**, scegliere una dimensione di macchina virtuale di SQL Server e revisione hello altre impostazioni.

* **Dimensioni della macchina virtuale SQL Server** dimensioni hello per entrambe le macchine virtuali che eseguono SQL Server. Scegliere le dimensioni più appropriate della macchina virtuale per il carico di lavoro. Se si compila questo ambiente per l'esercitazione hello, utilizzare **DS2**. Per i carichi di lavoro, scegliere una dimensione di macchina virtuale in grado di supportare il carico di lavoro di hello. Molti carichi di lavoro di produzione richiedono dimensioni **DS4** o superiori. modello Hello compila due macchine virtuali di queste dimensioni e installa SQL Server su ciascuna di esse. Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Hello Azure installa SQL Server Enterprise Edition. costo Hello dipende dall'edizione hello e dimensioni della macchina virtuale hello. Per informazioni dettagliate sui costi correnti, vedere [Prezzi di macchine virtuali](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Dimensioni macchina virtuale del controller di dominio** sono di dimensioni della macchina virtuale per hello hello i controller di dominio. Per questa esercitazione usare **D2**.
* **Dimensioni di macchina virtuale Witness di condivisione file** hello dimensioni di macchina virtuale per il controllo di condivisione file hello. Per questa esercitazione usare **A1**.
* **Account di archiviazione SQL** nome hello hello dell'account di archiviazione che contiene i dati di SQL Server hello e dischi del sistema operativo. Per questa esercitazione usare **alwaysonsql01**.
* **Account di archiviazione di controller di dominio** è hello nome dell'account di archiviazione hello hello i controller di dominio. Per questa esercitazione usare **alwaysondc01**.
* **Dimensioni del disco dati di SQL Server** in TB è dimensioni hello del disco dati di SQL Server hello in TB. Specificare un numero compreso tra 1 e 4. Per questa esercitazione usare **1**.
* **Ottimizzazione dell'archiviazione** imposta le impostazioni di configurazione di archiviazione specifiche per macchine virtuali di SQL Server hello in base al tipo di carico di lavoro hello. Tutte le macchine virtuali di SQL Server in questo scenario usare l'archiviazione premium con disco di Azure imposta solo tooread cache dell'host. Inoltre, è possibile ottimizzare le impostazioni di SQL Server per il carico di lavoro hello scegliendo una di queste tre impostazioni:

  * **Carico di lavoro generale**: non definisce impostazioni di configurazione specifiche.
  * **Elaborazione transazionale**: imposta i flag di traccia 1117 e 1118.
  * **Data warehousing**: imposta i flag di traccia 1117 e 610.

Per questa esercitazione usare **Carico di lavoro generale**.

![Impostazioni archiviazione dimensione VM](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Rivedere le impostazioni di hello e quindi fare clic su **OK**.

#### <a name="a-note-about-storage"></a>Nota sull'archiviazione
Ulteriori ottimizzazioni dipendono dalla dimensione di hello dei dischi dati di SQL Server hello. Per ogni terabyte di disco dati, Azure aggiunge un extra 1 TB di archiviazione Premium. Quando un server richiede 2 TB o più, hello modello consente di creare un pool di archiviazione in ogni macchina virtuale di SQL Server. Un pool di archiviazione è un modulo di virtualizzazione dell'archiviazione in cui più dischi sono configurati tooprovide maggiore capacità, resilienza e prestazioni.  modello Hello crea uno spazio di archiviazione nel pool di archiviazione hello e presenta un sistema operativo toohello di dati singolo disco. modello Hello designa il disco come disco dati hello per SQL Server. modello Hello ottimizza il pool di archiviazione hello per SQL Server utilizzando hello seguenti impostazioni:

* Dimensione di striping è hello interleave impostazione per il disco virtuale hello. I carichi di lavoro transazionali usano 64 KB. I carichi di lavoro del warehouse di dati usano 256 KB.
* Resilienza: nessuna resilienza.

> [!NOTE]
> Archiviazione premium di Azure localmente ridondante e mantiene tre copie dei dati hello in una singola regione, pertanto non è necessaria la resilienza aggiuntiva al pool di archiviazione hello.
>
>

* Numero di colonne è uguale a numero hello dei dischi nel pool di archiviazione hello.

Per altre informazioni sullo spazio di archiviazione e sui pool di archiviazione, vedere:

* [Panoramica di spazi di archiviazione](http://technet.microsoft.com/library/hh831739.aspx)
* [Windows Server Backup e pool di archiviazione](http://technet.microsoft.com/library/dn390929.aspx)

Per altre informazioni sulle procedure consigliate per la configurazione di SQL Server, vedere [Procedure consigliate per le prestazioni per SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Impostazioni di SQL Server
In **impostazioni di SQL Server**, esaminare e modificare prefisso del nome di macchina virtuale SQL Server hello, versione di SQL Server, account del servizio SQL Server e la password e hello l'applicazione automatica patch pianificazione della manutenzione di SQL.

* **Prefisso di nome di Server SQL** è toocreate utilizzati un nome per ogni macchina virtuale di SQL Server. Per questa esercitazione usare **sqlserver**. Hello modello nomi hello macchine virtuali di SQL Server *sqlserver 0* e *sqlserver 1*.
* **Versione di SQL Server** hello versione di SQL Server. Per questa esercitazione usare **SQL Server 2014**. È anche possibile scegliere **SQL Server 2012** o **SQL Server 2016**.
* **Nome utente account del servizio SQL Server** hello nome di account di dominio per hello servizio SQL Server. Per questa esercitazione usare **sqlservice**.
* **Password** password hello per hello account del servizio SQL Server.  Usare una password complessa. Conferma password hello.
* **Pianificazione della manutenzione di SQL l'applicazione automatica patch** identifica il giorno hello della settimana hello che Azure corregge automaticamente hello SQL Server. Per questa esercitazione digitare **Sunday** (domenica).
* **Ora di inizio manutenzione l'applicazione automatica patch SQL** è ora hello del giorno per hello regione di Azure quando si avvia l'applicazione automatica di patch.

> [!NOTE]
> l'applicazione di patch finestra per ogni macchina virtuale Hello avviene a fasi di un'ora. Solo una macchina virtuale è una patch a un'interruzione di tooprevent tempo dei servizi.
>
>

![Impostazioni di SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Rivedere le impostazioni di hello e quindi fare clic su **OK**.

### <a name="summary"></a>Riepilogo
Nella pagina Riepilogo hello Azure convalida le impostazioni di hello. È anche possibile scaricare il modello di hello. Riepilogo hello di revisione. Fare clic su **OK**.

### <a name="buy"></a>Acquistare
Questo pannello finale contiene le **condizioni d'uso** e l'**informativa sulla privacy**. Esaminare le informazioni. Quando si è pronti per le macchine virtuali di Azure toostart toocreate hello tutti hello altre risorse richieste per il gruppo di disponibilità hello fare clic su **crea**.

Hello portale di Azure Crea gruppo di risorse hello e tutte le risorse di hello.

## <a name="monitor-deployment"></a>Monitorare la distribuzione
Monitorare lo stato di distribuzione hello da hello portale di Azure. Un'icona che rappresenta la distribuzione di hello viene automaticamente aggiunto toohello dashboard del portale di Azure.

![Dashboard di Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Connettersi tooSQL Server
le nuove istanze Hello di SQL Server sono in esecuzione nelle macchine virtuali che dispongono degli indirizzi IP connesso a internet. È possibile remote desktop (RDP) direttamente tooeach macchina virtuale SQL Server.

tooRDP tooa SQL Server, seguire questi passaggi:

1. Da hello dashboard del portale di Azure, verificare che la distribuzione di hello ha avuto esito positivo.
2. Fare clic su **Risorse**.
3. In hello **risorse** pannello, fare clic su **sqlserver 0**, ovvero il nome computer hello di una delle macchine virtuali hello che esegue SQL Server.
4. Nel Pannello di hello per **sqlserver 0**, fare clic su **Connetti**. Il browser viene chiesto se si desidera tooopen o salvare un oggetto di connessione remota hello. Fare clic su **Apri**.
5. **Connessione desktop remoto** potrebbe informare l'utente che hello Impossibile identificare l'autore della connessione remota. Fare clic su **Connetti**.
6. Sicurezza di Windows richiede tooenter è l'indirizzo IP di credenziali tooconnect toohello hello primario del controller di dominio. Fare clic su **Usa un altro account**. In **Nome utente** digitare **contoso\DomainAdmin**. Questo account è stato configurato quando si imposta il nome utente amministratore di hello nel modello di hello. Utilizzare password complesse di hello scelto quando è stato configurato il modello di hello.
7. **Desktop remoto** venga avvisati del fatto che il computer remoto hello non è stato possibile autenticare scadenza tooproblems con il certificato di sicurezza. Mostra nome del certificato di sicurezza hello. Se si sono seguite esercitazione hello, nome hello è **sqlserver 0.contoso.com**. Fare clic su **Sì**.

Si è connessi con la macchina virtuale di SQL Server toohello RDP. È possibile aprire SQL Server Management Studio, connettersi toohello di istanza predefinita di SQL Server e verificare che tale gruppo di disponibilità hello è configurato.
