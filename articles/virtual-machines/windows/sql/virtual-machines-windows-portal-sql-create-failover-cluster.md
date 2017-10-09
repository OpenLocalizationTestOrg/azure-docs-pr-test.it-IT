---
title: aaaSQL FCI Server - macchine virtuali di Azure | Documenti Microsoft
description: Questo articolo viene illustrato come toocreate istanza di Cluster di Failover SQL Server in macchine virtuali di Azure.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Configurare l'istanza del cluster di failover di SQL Server nelle macchine virtuali di Azure

Questo articolo viene illustrato come toocreate un SQL Server del Cluster di Failover (FCI) di istanza su macchine virtuali nel modello di gestione risorse di Azure. Questa soluzione Usa [spazi di archiviazione diretta di Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) come una SAN virtuale basata su software che sincronizza l'archiviazione hello (dischi di dati) tra i nodi hello (macchine virtuali di Azure) in un Cluster di Windows. S2D è una novità di Windows Server 2016.

Hello diagramma seguente illustra la soluzione completa di hello in macchine virtuali di Azure:

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Hello precedente diagramma illustra:

- Due macchine virtuali di Azure in un cluster di failover di Windows. Una macchina virtuale in un cluster di failover è detta anche *nodo del cluster* o *nodo*.
- Ogni macchina virtuale ha due o più dischi dati.
- S2D Sincronizza i dati di hello nel disco dati hello e presenta una risorsa di archiviazione hello sincronizzato con un pool di archiviazione.
- pool di archiviazione Hello presenta un cluster di failover cluster toohello volume condiviso (CSV).
- ruolo del cluster di SQL Server FCI Hello Usa CSV hello per le unità dati hello.
- Un carico di Azure del servizio di bilanciamento toohold hello indirizzo IP per hello istanza cluster di failover di SQL Server.
- Un set di disponibilità di Azure contiene tutte le risorse di hello.

   >[!NOTE]
   >Tutte le risorse di Azure sono nel diagramma hello in hello stesso gruppo di risorse.

Per informazioni dettagliate su S2D, vedere l'articolo relativo a [Spazi di archiviazione diretta \(S2D\) in Windows Server 2016 Datacenter Edition](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D supporta due tipi di architettura: con convergenza e con iperconvergenza. architettura di Hello in questo documento è iperconvergente. Un archivio di hello iperconvergente infrastruttura posizioni in hello stessi server applicazione hello cluster host. In questa architettura, archiviazione hello è in ogni nodo dell'istanza cluster di failover di SQL Server.

### <a name="example-azure-template"></a>Modello di Azure di esempio

È possibile creare l'intera soluzione hello in Azure da un modello. Un esempio di un modello è disponibile in GitHub hello [modelli di avvio rapido di Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Questo esempio non è progettato né testato per carichi di lavoro specifici. È possibile eseguire hello modello toocreate una FCI di SQL Server con dominio di S2D archiviazione tooyour connesso. È possibile valutare il modello di hello e modificarla in base alle proprie esigenze.

## <a name="before-you-begin"></a>Prima di iniziare

Ci sono alcuni aspetti che occorre tooknow e un paio di aspetti che è necessario presenti prima di procedere.

### <a name="what-tooknow"></a>Quali tooknow
È necessario avere una conoscenza operativa di hello seguenti tecnologie:

- [Tecnologie cluster di Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Istanze del cluster di failover di SQL Server](http://msdn.microsoft.com/library/ms189134.aspx)

Inoltre, si deve avere una conoscenza generale di hello seguenti tecnologie:

- [Soluzione iperconvergente che usa Spazi di archiviazione diretta in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Gruppi di risorse di Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Quali toohave

Prima di seguire le istruzioni di hello in questo articolo, dovrebbe già disporre:

- Una sottoscrizione di Microsoft Azure.
- Un dominio Windows in macchine virtuali di Azure.
- Un account con gli oggetti di autorizzazione toocreate in hello macchina virtuale di Azure.
- Una rete virtuale di Azure e una subnet con sufficiente spazio degli indirizzi IP per hello seguenti componenti:
   - Entrambe le macchine virtuali.
   - indirizzo IP del cluster failover Hello.
   - Indirizzo IP per ogni istanza del cluster di failover.
- DNS configurato nella rete di Azure, verso i controller di dominio toohello hello.

Dopo aver soddisfatto questi prerequisiti, è possibile procedere con la creazione del cluster di failover. primo passaggio Hello è toocreate hello le macchine virtuali.

## <a name="step-1-create-virtual-machines"></a>Passaggio 1: Creare le macchine virtuali

1. Accedi toohello [portale di Azure](http://portal.azure.com) con la sottoscrizione.

1. [Creare un set di disponibilità di Azure](../tutorial-availability-sets.md).

   disponibilità Hello impostare macchine virtuali in domini di errore e domini di aggiornamento. set di disponibilità Hello garantiscono che l'applicazione non è influenzata da singoli punti di errore, ad esempio switch di rete hello o unità di alimentazione hello di un rack di server.

   Se non è stato creato il gruppo di risorse hello per le macchine virtuali, è possibile farlo quando si crea un set di disponibilità di Azure. Se si utilizza set di disponibilità hello hello toocreate portale Azure, hello i passaggi seguenti:

   - Nel portale di Azure hello, fare clic su  **+**  tooopen hello Azure Marketplace. Cercare **Set di disponibilità**.
   - Fare clic su **Set di disponibilità**.
   - Fare clic su **Crea**.
   - In hello **creare set di disponibilità** pannello hello set seguenti valori:
      - **Nome**: un nome per il set di disponibilità hello.
      - **Sottoscrizione**: sottoscrizione di Azure.
      - **Gruppo di risorse**: toouse un gruppo esistente, fare clic su **utilizzare esistente** e gruppo hello selezionare dall'elenco a discesa hello. In caso contrario scegliere **Crea nuovo** e digitare un nome per il gruppo di hello.
      - **Percorso**: impostare il percorso di hello in cui si prevede di toocreate le macchine virtuali.
      - **Domini di errore**: hello predefinito (3).
      - **Domini di aggiornamento**: hello predefinito (5).
   - Fare clic su **crea** toocreate hello set di disponibilità.

1. Creare macchine virtuali hello in set di disponibilità hello.

   Eseguire il provisioning di due macchine virtuali di SQL Server nel set di disponibilità di Azure hello. Per istruzioni, vedere [il provisioning di una macchina virtuale di SQL Server nel portale di Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

   Inserire entrambe le macchine virtuali:

   - In hello stesso gruppo di risorse di Azure imposta la disponibilità è.
   - In hello nella stessa rete del controller di dominio.
   - In una subnet con spazio indirizzi IP sufficiente per entrambe le macchine virtuali e tutte le istanze del cluster di failover che si potrebbero usare nel cluster.
   - Nel set di disponibilità di Azure hello.   

      >[!IMPORTANT]
      >Non è possibile impostare o modificare il set di disponibilità dopo che è stata creata una macchina virtuale.

   Scegliere un'immagine da hello Azure Marketplace. È possibile utilizzare un Marketplace immagine con che include solo hello Windows Server e SQL Server o Windows Server. Per informazioni dettagliate, vedere [Panoramica di SQL Server in macchine virtuali di Azure](../../virtual-machines-windows-sql-server-iaas-overview.md).

   immagini di SQL Server in hello raccolta Azure ufficiale Hello includono un'istanza di SQL Server installata, oltre a software di installazione di SQL Server hello e chiave obbligatoria hello.

   Scegliere l'immagine a destra hello in base a toohow desiderato toopay di licenza di SQL Server hello:

   - **Pagare le licenze di utilizzo per**: costo al minuto hello di queste immagini include hello licenza di SQL Server:
      - **SQL Server 2016 Enterprise in Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard in Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer in Windows Server Datacenter 2016**

   - **BYOL (Bring Your Own License)**

      - **{BYOL} SQL Server 2016 Enterprise in Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard in Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Dopo aver creato una macchina virtuale hello, rimuovere l'istanza di SQL Server hello pre-installata in modalità autonoma. Dopo aver configurato il cluster di failover di hello e S2D, si utilizzerà hello pre-installato SQL Server supporti toocreate hello istanza cluster di failover di SQL Server.

   In alternativa, è possibile utilizzare le immagini di Azure Marketplace con solo hello del sistema operativo. Scegliere un **Data Center di Windows Server 2016** installa hello istanza cluster di failover di SQL Server dopo aver configurato il cluster di failover di hello e S2D e immagini. Un'immagine di questo tipo non contiene i supporti di installazione di SQL Server. Inserire il supporto di installazione di hello in una posizione in cui è possibile eseguire l'installazione di SQL Server hello per ogni server.

1. Dopo la creazione delle macchine virtuali di Azure, è possibile connettere macchina virtuale tooeach con RDP.

   Quando ci si connette prima macchina virtuale tooa con RDP, computer hello chiede se si desidera tooallow toobe questo PC individuabile in rete hello. Fare clic su **Sì**.

1. Se si utilizza una delle immagini di macchina virtuale basata su SQL Server hello, rimuovere l'istanza di SQL Server hello.

   - In **Programmi e funzionalità** fare clic con il pulsante destro del mouse su **Microsoft SQL Server 2016 (64 bit)** e scegliere **Disinstalla/Cambia**.
   - Fare clic su **Rimuovi**.
   - Selezionare l'istanza predefinita di hello.
   - Rimuovere tutte le funzionalità in **Servizi motore di database**. Non rimuovere **Funzionalità condivise**. Vedere hello seguente immagine:

      ![Rimuovere le funzionalità](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Fare clic su **Avanti** e quindi su **Rimuovi**.

1. <a name="ports"></a>Aprire le porte del firewall hello.

   In ogni macchina virtuale, aprire hello seguendo porte hello Windows Firewall.

   | Scopo | Porta TCP | Note
   | ------ | ------ | ------
   | SQL Server | 1433 | Porta normale per le istanze predefinite di SQL Server. Se si utilizza un'immagine dalla raccolta di hello, questa porta viene aperta automaticamente.
   | Probe di integrità | 59999 | Qualsiasi porta TCP aperta. In un passaggio successivo, configurare il bilanciamento del carico di hello [probe di integrità](#probe) e hello cluster toouse questa porta.  

1. Aggiungere una macchina virtuale di archiviazione toohello. Per informazioni dettagliate, vedere l'articolo relativo all'[aggiunta dell'archiviazione](../../../storage/common/storage-premium-storage.md).

   Entrambe le macchine virtuali necessitano di almeno due dischi dati.

   Collegare dischi non formattati, ossia senza formattazione NTFS.
      >[!NOTE]
      >Se si collegano dischi con formattazione NTFS, è possibile abilitare S2D solo senza controllo dell'idoneità del disco.  

   Collegare un minimo di due archiviazione Premium (dischi SSD) tooeach macchina virtuale. È consigliabile usare almeno dischi P30 (da 1 TB).

   Host di impostare la memorizzazione nella cache troppo**Read-only**.

   capacità di archiviazione Hello che è usare negli ambienti di produzione dipende dal carico di lavoro. i valori Hello descritti in questo articolo sono per la dimostrazione e test.

1. [Aggiungere hello macchine virtuali tooyour preesistente dominio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Dopo che le macchine virtuali hello create e configurate, è possibile configurare cluster di failover hello.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Passaggio 2: Configurare il Cluster di Failover di Windows hello con S2D

passaggio successivo Hello è di tipo cluster di failover di hello tooconfigure con S2D. In questo passaggio si eseguiranno hello seguenti passaggi:

1. Aggiungere la funzionalità Clustering di failover di Windows
1. Convalida cluster hello
1. Creare il cluster di failover di hello
1. Creare server di controllo di hello cloud
1. Aggiungere le risorse di archiviazione

### <a name="add-windows-failover-clustering-feature"></a>Aggiungere la funzionalità Clustering di failover di Windows

1. toobegin, connettersi toohello prima macchina virtuale con RDP utilizzando un account di dominio membro del gruppo administrators locale, che contiene oggetti toocreate di autorizzazioni in Active Directory. Utilizzare questo account per il resto di hello della configurazione di hello.

1. [Aggiungere il Clustering di Failover di macchina virtuale tooeach funzionalità](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   funzionalità Clustering di Failover tooinstall dall'interfaccia utente, hello hello in entrambe le macchine virtuali come segue.
   - In **Server Manager** fare clic su **Gestione** e quindi su **Aggiungi ruoli e funzionalità**.
   - In **Aggiunta guidata ruoli e funzionalità**, fare clic su **Avanti** fino a ottenere troppo**Seleziona funzionalità**.
   - In **Selezione funzionalità** selezionare **Clustering di failover**. Includere tutti gli strumenti di gestione di hello e le funzionalità necessarie. Fare clic su **Aggiungi funzionalità**.
   - Fare clic su **Avanti** e quindi fare clic su **fine** funzionalità hello tooinstall.

   tooinstall hello funzionalità Clustering di Failover con PowerShell, eseguire lo script da una sessione di PowerShell amministratore seguente in una delle macchine virtuali hello hello.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Per riferimento, i passaggi successivi hello seguono le istruzioni di hello nel passaggio 3 di [soluzione convergente Hyper tramite spazi di archiviazione diretta in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Convalida cluster hello

Questa guida si riferisce tooinstructions in [convalida cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Convalida cluster hello in hello dell'interfaccia utente o con PowerShell.

cluster di hello toovalidate con interfaccia utente, hello hello seguendo i passaggi da una delle macchine virtuali hello.

1. In **Server Manager** fare clic su **Strumenti** e quindi su **Gestione cluster di failover**.
1. In **Gestione cluster di failover** fare clic su **Azione** e quindi su **Convalida configurazione**.
1. Fare clic su **Avanti**.
1. In **selezionare Server o un Cluster**, nome del tipo hello di entrambe le macchine virtuali.
1. In **Opzioni di testing** scegliere **Esegui solo test selezionati**. Fare clic su **Avanti**.
1. In **Selezione dei test** includere tutti i test tranne **Archiviazione**. Vedere hello seguente immagine:

   ![Test di convalida](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Fare clic su **Avanti**.
1. In **Conferma** fare clic su **Avanti**.

Hello **convalida guidata configurazione** hello di esecuzioni di test di convalida.

cluster di hello toovalidate con PowerShell, eseguire lo script da una sessione di PowerShell amministratore seguente in una delle macchine virtuali hello hello.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Dopo la convalida del cluster di hello, creare il cluster di failover di hello.

### <a name="create-hello-failover-cluster"></a>Creare il cluster di failover di hello

Questa guida si riferisce troppo[Crea cluster di failover hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

cluster di failover hello toocreate, è necessario:
- i nomi di Hello delle macchine virtuali hello che diventano hello i nodi del cluster.
- Un nome per il cluster di failover di hello
- Un indirizzo IP per il cluster di failover di hello. È possibile utilizzare un indirizzo IP non usato in hello stessa rete virtuale e subnet come hello i nodi del cluster.

Hello PowerShell seguente crea un cluster di failover. Aggiornare lo script hello con nomi di hello dei nodi di hello (nomi di macchina virtuale hello) e un indirizzo IP disponibile da hello rete virtuale di Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Creare un cloud di controllo

Il cloud di controllo è un nuovo tipo di quorum di controllo del cluster archiviato in un BLOB del servizio di archiviazione di Azure. Ciò consente di rimuovere hello necessità di una macchina virtuale separata che ospita una condivisione di controllo.

1. [Creare un cloud di controllo per il cluster di failover di hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Creare un contenitore BLOB.

1. Salvare le chiavi di accesso hello e hello URL del contenitore.

1. Configurare hello del quorum di cluster di failover cluster controllo. Vedere [Configura hello quorum di controllo nell'interfaccia utente di hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello dell'interfaccia utente.

### <a name="add-storage"></a>Aggiungere le risorse di archiviazione

i dischi di Hello per S2D devono toobe vuoto e senza partizioni o altri dati. seguono i dischi tooclean [hello i passaggi in questa Guida](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Abilitare Spazi di archiviazione diretta \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Hello PowerShell seguente consente di spazi di archiviazione diretti.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   In **gestione Cluster di Failover**, è ora possibile visualizzare i pool di archiviazione hello.

1. [Creare un volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Una delle funzionalità di hello di S2D è che viene creato automaticamente un pool di archiviazione quando si attiva un. Si è ora pronto toocreate un volume. cmdlet PowerShell di Hello `New-Volume` automatizza hello volume creazione processo, tra cui la formattazione, aggiunta toohello cluster e la creazione di un volume condiviso cluster (CSV). Hello di esempio seguente crea un 800 gigabyte (GB) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Al termine dell'esecuzione del comando, un volume di 800 GB viene montato come risorsa cluster. volume Hello è `C:\ClusterStorage\Volume1\`.

   Hello seguente diagramma viene illustrato un volume condiviso cluster con S2D:

   ![Volume condiviso cluster](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Passaggio 3: Testare il failover del cluster di failover

In Gestione Cluster di Failover, verificare che è possibile spostare toohello risorse di archiviazione hello altro nodo del cluster. Se è possibile connettere i cluster di failover toohello con **gestione Cluster di Failover** e spostare archiviazione hello da un nodo toohello altre, si è pronti tooconfigure hello FCI.

## <a name="step-4-create-sql-server-fci"></a>Passaggio 4: Creare l'istanza del cluster di failover di SQL Server

Dopo aver configurato il cluster di failover di hello e tutti i componenti di cluster, inclusa l'archiviazione, è possibile creare hello istanza cluster di failover di SQL Server.

1. Connettere toohello prima macchina virtuale con il protocollo RDP.

1. In **gestione Cluster di Failover**, assicurarsi che tutte le risorse principali del cluster siano presenti hello prima macchina virtuale. Se necessario, spostare una macchina virtuale di tutte le risorse toothis.

1. Individuare il supporto di installazione di hello. Se usato nella macchina virtuale hello delle immagini di Azure Marketplace hello, si trova in media hello `C:\SQLServer_<version number>_Full`. Fare clic su **Configura**.

1. In hello **Centro installazione SQL Server**, fare clic su **installazione**.

1. Fare clic su **Installazione di un nuovo cluster di failover di SQL Server**. Seguire le istruzioni hello hello tooinstall tramite procedura guidata hello istanza cluster di failover di SQL Server.

   directory dei dati dell'istanza FCI Hello necessario toobe nell'archiviazione cluster. Con S2D, non è un disco condiviso, ma un volume tooa punto di montaggio in ogni server. S2D Sincronizza volume hello tra entrambi i nodi. volume Hello viene presentato toohello cluster come volume condiviso cluster. Utilizzo di punto di montaggio CSV hello per le directory dati hello.

   ![Directory di dati](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Dopo aver completato la procedura guidata hello, verrà installato nel primo nodo hello una FCI di SQL Server.

1. Dopo l'installazione hello FCI nel primo nodo hello correttamente, è possibile connettere toohello secondo nodo con RDP.

1. Aprire hello **Centro installazione SQL Server**. Fare clic su **Installazione**.

1. Fare clic su **cluster di failover di SQL Server di Aggiungi nodo tooa**. Seguire le istruzioni hello del server SQL tooinstall guidata hello e aggiungere questo toohello server FCI.

   >[!NOTE]
   >Se si utilizza un'immagine della raccolta Azure Marketplace con SQL Server, strumenti di SQL Server sono stati inclusi con l'immagine di hello. Se non è stata utilizzata questa immagine, è possibile installare separatamente gli strumenti di SQL Server hello. Vedere [Scaricare SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Passaggio 5: Creare un servizio di bilanciamento del carico di Azure

Macchine virtuali di Azure, i cluster utilizzano un toohold del servizio di bilanciamento carico di un indirizzo IP che deve toobe su un nodo cluster alla volta. In questa soluzione, bilanciamento del carico hello contiene l'indirizzo IP hello hello istanza cluster di failover di SQL Server.

[Creare e configurare un servizio di bilanciamento del carico di Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Creare servizio di bilanciamento del carico hello in hello portale di Azure

bilanciamento del carico di hello toocreate:

1. Nel portale di Azure hello, passare toohello gruppo di risorse con le macchine virtuali hello.

1. Fare clic su **+ Aggiungi**. Hello ricerca Marketplace per **bilanciamento del carico**. Fare clic su **Servizio di bilanciamento del carico**.

1. Fare clic su **Crea**.

1. Configurare il bilanciamento del carico hello con:

   - **Nome**: un nome che identifichi bilanciamento del carico hello.
   - **Tipo**: servizio di bilanciamento del carico hello possa essere pubblici o privati. Un servizio di bilanciamento del carico privato è accessibile dall'interno hello stessa rete virtuale. La maggior parte delle applicazioni Azure può usare un servizio di bilanciamento del carico privato. Se l'applicazione deve accedere tooSQL Server direttamente su Internet hello, utilizzare un servizio di bilanciamento del carico pubblico.
   - **Rete virtuale**: hello stessa rete hello le macchine virtuali.
   - **Subnet**: hello stessa subnet hello le macchine virtuali.
   - **Indirizzo IP privato**: hello stesso indirizzo IP assegnato risorsa di rete cluster toohello istanza cluster di failover di SQL Server.
   - **Sottoscrizione**: sottoscrizione di Azure.
   - **Gruppo di risorse**: utilizzare hello stesso gruppo di risorse come le macchine virtuali.
   - **Percorso**: utilizzare hello stesso percorso di Azure le macchine virtuali.
   Vedere hello seguente immagine:

   ![Creare il servizio di bilanciamento del carico](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Configurare i pool back-end di bilanciamento del carico hello

1. Restituire toohello il gruppo di risorse di Azure con le macchine virtuali hello e individuare di nuovo bilanciamento del carico hello. È possibile visualizzare hello toorefresh su hello gruppo di risorse. Fare clic su servizio di bilanciamento del carico hello.

1. Nel pannello del servizio di bilanciamento carico di hello, fare clic su **pool back-end**.

1. Fare clic su **+ Aggiungi** tooadd un pool back-end.

1. Digitare un nome per il pool back-end hello.

1. Fare clic su **Aggiungi una macchina virtuale**.

1. In hello **scegliere macchine virtuali** pannello, fare clic su **scegliere un set di disponibilità**.

1. Scegliere set di disponibilità di hello è inserito di macchine virtuali di SQL Server hello in.

1. In hello **scegliere macchine virtuali** pannello, fare clic su **scegliere macchine virtuali hello**.

   Il portale di Azure dovrebbe essere simile hello seguente immagine:

   ![Creare il back-end del servizio di bilanciamento di carico](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Fare clic su **selezionare** su hello **scegliere macchine virtuali** blade.

1. Fare clic su **OK** due volte.

### <a name="configure-a-load-balancer-health-probe"></a>Configurare un probe di integrità per il servizio di bilanciamento del carico

1. Nel pannello del servizio di bilanciamento carico di hello, fare clic su **probe di integrità**.

1. Fare clic su **+ Aggiungi**.

1. In hello **probe di integrità Aggiungi** pannello <a name="probe"> </a>impostare i parametri di probe di integrità hello:

   - **Nome**: un nome per il probe di integrità hello.
   - **Protocollo**: TCP.
   - **Porta**: impostare tooan porta TCP disponibile. È necessaria una porta del firewall aperta. Hello utilizzare [stessa porta](#ports) viene impostata per il probe di integrità hello in firewall hello.
   - **Intervallo**: 5 secondi.
   - **Soglia di non integrità**: 2 errori consecutivi.

1. Fare clic su OK.

### <a name="set-load-balancing-rules"></a>Impostare le regole di bilanciamento del carico

1. Nel pannello del servizio di bilanciamento carico di hello, fare clic su **regole di bilanciamento del carico**.

1. Fare clic su **+ Aggiungi**.

1. Impostare hello i parametri regole di bilanciamento del carico:

   - **Nome**: un nome per le regole di bilanciamento del carico di hello.
   - **Indirizzo IP Frontend**: utilizzare l'indirizzo IP hello per hello risorsa di rete del cluster di failover di SQL Server.
   - **Porta**: impostare per la porta TCP di SQL Server FCI hello. porta dell'istanza Hello predefinita è 1433.
   - **Porta back-end**: questo valore utilizza hello stessa porta come hello **porta** valore quando si abilita **IP mobile (direct server restituito)**.
   - **Pool back-end**: utilizzare hello back-end nome del pool configurata in precedenza.
   - **Probe di integrità**: probe di integrità hello utilizzare configurata in precedenza.
   - **Salvataggio permanente sessione**: Nessuno.
   - **Timeout di inattività (minuti)**: 4.
   - **IP mobile (Direct Server Return)**: Abilitato.

1. Fare clic su **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Passaggio 6: Configurare il cluster per il probe

Impostare parametro porta probe di cluster hello in PowerShell.

tooset hello parametro porta probe di cluster, aggiornare le variabili in hello lo script seguente dall'ambiente in uso.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Passaggio 7: Eseguire il failover dell'istanza del cluster di failover

Failover di test della funzionalità cluster di failover toovalidate hello. Hello i passaggi seguenti:

1. Connettere tooone dei nodi del cluster di failover di SQL Server hello con RDP.

1. Aprire **Gestione cluster di failover**. Fare clic su **Ruoli**. Nota: il nodo detiene il ruolo di SQL Server FCI hello.

1. Fare clic sul ruolo di hello istanza cluster di failover di SQL Server.

1. Scegliere **Sposta** e quindi fare clic su **Miglior nodo possibile**.

**Gestione Cluster di failover** Mostra hello ruolo e le relative risorse offline. Hello risorse spostare e portare in linea in hello altro nodo.

### <a name="test-connectivity"></a>Testare la connettività

connettività tootest, log nella macchina virtuale tooanother hello stessa rete virtuale. Aprire **SQL Server Management Studio** e connettersi toohello nome di istanza cluster di failover di SQL Server.

>[!NOTE]
>Se necessario, è possibile [scaricare SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Limitazioni
Nelle macchine virtuali di Azure, Microsoft Distributed Transaction Coordinator (DTC) non è supportata nella FCI perché hello porta RPC non è supportato dal servizio di bilanciamento del carico hello.

## <a name="see-also"></a>Vedere anche

[Configurare S2D con Desktop remoto (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Soluzione iperconvergente che usa Spazi di archiviazione diretta](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Panoramica di Spazi di archiviazione diretta](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Supporto di SQL Server per S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
