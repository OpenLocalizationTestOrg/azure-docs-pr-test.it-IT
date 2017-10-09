---
title: "Gruppi di disponibilità Server - macchine virtuali di Azure - esercitazione aaaSQL | Documenti Microsoft"
description: "Questa esercitazione viene illustrato come toocreate un SQL Server gruppo di disponibilità AlwaysOn in macchine virtuali di Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configurare manualmente un gruppo di disponibilità AlwaysOn in VM di Azure

Questa esercitazione viene illustrato come toocreate un SQL Server gruppo di disponibilità AlwaysOn in macchine virtuali di Azure. esercitazione completa Hello crea un gruppo di disponibilità con una replica di database in due computer SQL Server.

**Tempo stimato**: accetta toocomplete circa 30 minuti, una volta soddisfatti i prerequisiti di hello.

diagramma di Hello illustra ciò che si compila in esercitazione hello.

![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Prerequisiti

esercitazione Hello presuppone di che avere una conoscenza di base di SQL Server di gruppi di disponibilità AlwaysOn. Se sono necessarie altre informazioni, vedere [Panoramica di Gruppi di disponibilità AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Hello nella tabella seguente elenca i prerequisiti di hello che è necessario toocomplete prima di iniziare questa esercitazione:

|  |Requisito |Descrizione |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Due istanze di SQL Server | - In un set di disponibilità di Azure <br/> - In un dominio singolo <br/> - Con la funzionalità Clustering di failover installata |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Controllo di condivisione file per il cluster |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Account del servizio SQL Server | Account di dominio |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Account del servizio SQL Server Agent | Account di dominio |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Porte del firewall aperte | - SQL Server: **1433** per l'istanza predefinita <br/> - Endpoint del mirroring del database: **5022** o qualsiasi porta disponibile <br/> - Probe di bilanciamento del carico di Azure: **59999** o qualsiasi porta disponibile |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Aggiunta della funzionalità Clustering di failover | Questa funzionalità è necessaria per entrambe le istanze di SQL Server |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Account di dominio dell'installazione | - Amministratore locale in ogni istanza di SQL Server <br/> - Membro del ruolo predefinito del server sysadmin di SQL Server per ogni istanza di SQL Server  |


Prima di iniziare l'esercitazione hello, è necessario troppo[completare i prerequisiti per la creazione di gruppi di disponibilità AlwaysOn in macchine virtuali di Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md). Se questi prerequisiti sono già completati, è possibile passare troppo[crea Cluster](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Creare il cluster hello

Dopo aver hello vengono soddisfatti i prerequisiti, hello primo passaggio consiste toocreate un Cluster di Failover di Windows Server che include due SQL Server e un server di controllo.  

1. RDP toohello prima di SQL Server utilizzando un account di dominio che un amministratore del server SQL sia il server di controllo di hello.

   >[!TIP]
   >Se si sono seguite hello [documento prerequisiti](virtual-machines-windows-portal-sql-availability-group-prereq.md), è stato creato un account denominato **CORP\Install**. Usare questo account.

2. In hello **Server Manager** dashboard, selezionare **strumenti**, quindi fare clic su **gestione Cluster di Failover**.
3. Nel riquadro di sinistra hello, fare doppio clic su **gestione Cluster di Failover**, quindi fare clic su **creare un Cluster**.
   ![Creare un cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. In Creazione guidata Cluster hello, creare un cluster a un nodo avanzando pagine hello con le impostazioni di hello in hello nella tabella seguente:

   | Page | Impostazioni |
   | --- | --- |
   | Prima di iniziare |Valori predefiniti |
   | Selezione dei server |Prima di SQL Server nome in hello di tipo **immettere il nome del server** e fare clic su **Aggiungi**. |
   | Avviso di convalida |Selezionare **Nr I non è necessario supporto da Microsoft per questo cluster e pertanto non si desidera che la convalida di hello toorun test. Quando fa clic su Avanti, continuare con la creazione di cluster hello**. |
   | Punto di accesso per hello amministrazione Cluster |Digitare un nome di cluster, ad esempio **SQLAGCluster1**, in **Nome cluster**.|
   | Conferma |Usare le impostazioni predefinite a meno a meno che non si usino spazi di archiviazione. Vedere la nota di hello segue questa tabella. |

### <a name="set-hello-cluster-ip-address"></a>Impostare l'indirizzo IP del cluster hello

1. In **gestione Cluster di Failover**, scorrere verso il basso troppo**risorse principali del Cluster** ed espandere i dettagli del cluster hello. Dovrebbe essere entrambi hello **nome** hello e **indirizzo IP** risorse hello **Failed** stato. Hello risorsa indirizzo IP non può essere portata online perché il cluster di hello è assegnato hello stesso indirizzo IP come macchina hello stessa, pertanto è un indirizzo duplicato.

2. Hello pulsante destro del mouse non è stato possibile **indirizzo IP** risorsa e quindi fare clic su **proprietà**.

   ![Proprietà del cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Selezionare **indirizzo IP statico** e specificare un indirizzo disponibile dalla subnet in cui SQL Server hello è nella casella di testo indirizzo hello. Fare quindi clic su **OK**.
4. In hello **risorse principali del Cluster** sezione, fare doppio clic su nome cluster e fare clic su **in linea**. Attendere finché entrambe le risorse non sono online Quando risorsa del nome cluster hello torna online, il server di controller di dominio hello viene aggiornato con un nuovo account computer di Active Directory. Utilizzare questo hello toorun di AD account servizio di gruppo di disponibilità in cluster in un secondo momento.

### <a name="addNode"></a>Aggiungere hello altri toocluster di SQL Server

Aggiungere altri cluster di SQL Server toohello hello.

1. Nell'albero di browser hello, fare doppio clic su cluster hello e fare clic su **aggiunta del nodo**.

    ![Aggiungere toohello nodo Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. In hello **Aggiunta guidata nodi**, fare clic su **Avanti**. In hello **selezione dei server** pagina, aggiungere hello secondo computer SQL Server. Nome del server di tipo hello in **immettere il nome del server** e quindi fare clic su **Aggiungi**. Al termine dell'operazione, scegliere **Avanti**.

1. In hello **avviso di convalida** pagina, fare clic su **n** (in uno scenario di produzione è necessario eseguire il test di convalida hello). Quindi fare clic su **Next**.

8. In hello **conferma** pagina se si utilizza spazi di archiviazione, con l'etichetta casella di controllo crittografato hello **aggiungere tutte le risorse di archiviazione idonee toohello cluster.**

   ![Confermare l'aggiunta del nodo](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Se si utilizza spazi di archiviazione e non si deseleziona **aggiungere tutte le risorse di archiviazione idonee toohello cluster**, Windows consente di scollegare i dischi virtuali hello durante il processo di clustering hello. Di conseguenza, essi non vengono visualizzati in Gestione disco o Esplora fino a quando non vengono rimossi gli spazi di archiviazione di hello dal cluster hello e ricollegati tramite PowerShell. Spazi di archiviazione consente di raggruppare più dischi nel pool di toostorage. Per altre informazioni, vedere [Spazi di archiviazione](https://technet.microsoft.com/library/hh831739).

1. Fare clic su **Avanti**.

1. Fare clic su **Finish**.

   Gestione Cluster di failover mostra che il cluster dispone di un nuovo nodo ed elencato in hello **nodi** contenitore.

10. Disconnettersi dalla sessione desktop remoto hello.

### <a name="add-a-cluster-quorum-file-share"></a>Aggiungere una condivisione file di quorum del cluster

In questo esempio il cluster di Windows hello Usa un toocreate di condivisione di un quorum di cluster di file. Questa esercitazione usa un quorum Maggioranza dei nodi e delle condivisioni file. Per altre informazioni, vedere [Informazioni sulle configurazioni quorum in un cluster di failover](http://technet.microsoft.com/library/cc731739.aspx).

1. Connettere i server membro di controllo della condivisione file toohello con una sessione desktop remoto.

1. In **Server Manager** fare clic su **Strumenti**. Aprire **Gestione computer**.

1. Fare clic su **Cartelle condivise**.

1. Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilizzare **creare una cartella condivisa** toocreate una condivisione.

1. In **percorso della cartella**, fare clic su **Sfoglia** e individuare o creare un percorso per la cartella condivisa di hello. Fare clic su **Avanti**.

1. In **nome, descrizione e le impostazioni** verificare il nome di condivisione hello e il percorso. Fare clic su **Avanti**.

1. In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**. Fare clic su **Personalizza**.

1. In **Personalizza autorizzazioni** fare clic su **Aggiungi**.

1. Verificare che il cluster di hello hello toocreate account utilizzato dispone del controllo completo.

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Fare clic su **OK**.

1. In **Autorizzazioni cartella condivisa** fare clic su **Fine**. Fare di nuovo clic su **Fine**.  

1. Disconnettersi da server hello

### <a name="configure-cluster-quorum"></a>Configurare il quorum del cluster

Quindi, impostare quorum del cluster hello.

1. Connettere toohello primo nodo del cluster con desktop remoto.

1. In **gestione Cluster di Failover**, fare doppio clic su cluster hello, scegliere troppo**altre azioni**, fare clic su **Configura impostazioni Quorum del Cluster...** .

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. In **Configurazione guidata quorum del cluster** fare clic su **Avanti**.

1. In **selezione opzione configurazione Quorum**, scegliere **selezione quorum di controllo hello**, fare clic su **Avanti**.

1. In **Selezione quorum di controllo** fare clic su **Configura condivisione file di controllo**.

   >[!TIP]
   >Windows Server 2016 supporta un cloud di controllo. Se si sceglie questo tipo di controllo, non è necessario un controllo di condivisione file. Per altre informazioni, vedere [Distribuire un cloud di controllo per un cluster di failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Questa esercitazione usa un controllo di condivisione file, supportato dai sistemi operativi precedenti.

1. In **configurazione Witness di condivisione File**, percorso hello del tipo per la condivisione di hello creata. Fare clic su **Avanti**.

1. Verificare le impostazioni di hello in **conferma**. Fare clic su **Avanti**.

1. Fare clic su **Finish**.

risorse principali del cluster Hello vengono configurate con una condivisione file di controllo.

## <a name="enable-availability-groups"></a>Abilitare i gruppi di disponibilità

Successivamente, abilitare hello **gruppi di disponibilità AlwaysOn** funzionalità. Eseguire questi passaggi in entrambe le istanze di SQL Server.

1. Da hello **avviare** schermata, avviare **Gestione configurazione SQL Server**.
2. Nella struttura di browser hello, fare clic su **servizi di SQL Server**, quindi fare doppio clic su hello **SQL Server (MSSQLSERVER)** del servizio e fare clic su **proprietà**.
3. Fare clic su hello **disponibilità elevata AlwaysOn** tab, quindi selezionare **Abilita gruppi di disponibilità AlwaysOn**, come segue:

    ![Abilitare Gruppi di disponibilità AlwaysOn in Azure](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Fare clic su **Apply**. Fare clic su **OK** nella finestra di dialogo popup hello.

5. Riavviare il servizio di SQL Server hello.

Ripetere questi passaggi in hello altro SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Creare un database in hello prima di SQL Server

1. Avvio hello RDP file toohello prima di SQL Server con un dominio dell'account che è un membro del ruolo sysadmin ruolo del server.
1. Aprire SQL Server Management Studio e connettersi toohello prima di SQL Server.
7. In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e scegliere **Nuovo database**.
8. In **Nome database** digitare **MyDB1**, quindi fare clic su **OK**.

### <a name="backupshare"></a> Creare una condivisione di backup

1. In hello prima di SQL Server in **Server Manager**, fare clic su **strumenti**. Aprire **Gestione computer**.

1. Fare clic su **Cartelle condivise**.

1. Fare clic con il pulsante destro del mouse su **Condivisioni** e scegliere **Nuova condivisione**.

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Utilizzare **creare una cartella condivisa** toocreate una condivisione.

1. In **percorso della cartella**, fare clic su **Sfoglia** e individuare o creare un percorso della cartella condivisa backup database hello. Fare clic su **Avanti**.

1. In **nome, descrizione e le impostazioni** verificare il nome di condivisione hello e il percorso. Fare clic su **Avanti**.

1. In **Autorizzazioni cartella condivisa** impostare **Personalizza autorizzazioni**. Fare clic su **Personalizza**.

1. In **Personalizza autorizzazioni** fare clic su **Aggiungi**.

1. Assicurarsi di disporre di un account di servizio di SQL Server e SQL Server Agent hello per entrambi i server di controllo completo.

   ![Nuova condivisione](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Fare clic su **OK**.

1. In **Autorizzazioni cartella condivisa** fare clic su **Fine**. Fare di nuovo clic su **Fine**.  

### <a name="take-a-full-backup-of-hello-database"></a>Eseguire un backup del database hello completo

È necessario tooback backup hello nuova database tooinitialize hello catena di log. Se non si adotta un backup del database nuovo hello, non può essere inclusa in un gruppo di disponibilità.

1. In **Esplora oggetti**, fare doppio clic su database hello, scegliere troppo**attività...** , fare clic su **backup**.

1. Fare clic su **OK** tootake un percorso di backup predefinito toohello backup completo.

## <a name="create-hello-availability-group"></a>Creare il gruppo di disponibilità hello
Si è ora pronto tooconfigure un gruppo di disponibilità utilizzando hello seguendo i passaggi:

* Creare un database in hello prima di SQL Server.
* Eseguire un backup completo e un backup del log delle transazioni del database hello
* Hello ripristino completo e toohello backup log secondo SQL Server con hello **NORECOVERY** opzione
* Creare il gruppo di disponibilità hello (**AG1**) con commit sincrono, il failover automatico e repliche secondarie leggibili

### <a name="create-hello-availability-group"></a>Creare il gruppo di disponibilità hello:

1. Nella sessione desktop remoto toohello prima di SQL Server. In **Esplora oggetti** in SSMS fare clic con il pulsante destro del mouse su **Disponibilità elevata AlwaysOn**, quindi scegliere **Creazione guidata Gruppo di disponibilità**.

    ![Avviare la creazione guidata nuovo gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. In hello **Introduzione** pagina, fare clic su **Avanti**. In hello **Specifica nome del gruppo di disponibilità** , digitare un nome per hello gruppo di disponibilità, ad esempio **AG1**nella **nome gruppo di disponibilità**. Fare clic su **Avanti**.

    ![Creazione guidata nuovo gruppo di disponibilità: specificare il nome di gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. In hello **Seleziona database** pagina, selezionare il database e fare clic su **Avanti**.

   >[!NOTE]
   >database Hello soddisfi i prerequisiti di hello per un gruppo di disponibilità perché non si è effettuato almeno un backup completo sulla replica primaria prevista hello.

   ![Creazione guidata nuovo gruppo di disponibilità: selezionare i database](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. In hello **specifica repliche** pagina, fare clic su **Aggiungi Replica**.

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Hello **connettersi tooServer** visualizzata la finestra di. Nome del secondo server di hello in hello di tipo **nome Server**. Fare clic su **Connetti**.

   In hello **specifica repliche** pagina, dovrebbe essere secondo server hello elencati in **le repliche di disponibilità**. Configurare le repliche di hello come indicato di seguito.

   ![Creazione guidata nuovo gruppo di disponibilità: specificare le repliche (complete)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Fare clic su **endpoint** toosee hello endpoint del mirroring per questo gruppo di disponibilità. Hello utilizzare stessa porta utilizzata quando si imposta hello [regola del firewall per endpoint di mirroring del database](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. In hello **seleziona sincronizzazione dati iniziale** selezionare **completo** e specificare un percorso di rete condivisa. Per il percorso di hello, utilizzare hello [condivisione di backup creato](#backupshare). Nell'esempio hello è **\\\\\<prima di SQL Server\>\Backup\**. Fare clic su **Avanti**.

   >[!NOTE]
   >Sincronizzazione completa richiede un backup completo del database hello in prima istanza di SQL Server del hello e ripristinarlo toohello seconda istanza. Per i database di grandi dimensioni, la sincronizzazione completa non è consigliabile perché può richiedere diverso tempo. Per ridurre questo momento, eseguire un backup del database hello manualmente e il ripristino con `NO RECOVERY`. Se il database di hello è già ripristinato con `NO RECOVERY` su hello secondo SQL Server prima di configurare il gruppo di disponibilità hello, scegliere **solo Join**. Se si desidera backup hello tootake dopo aver configurato il gruppo di disponibilità hello, scegliere **Ignora sincronizzazione dati iniziale**.

    ![Creazione guidata nuovo gruppo di disponibilità: selezionare la sincronizzazione dati iniziale](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. In hello **convalida** pagina, fare clic su **Avanti**. Questa pagina dovrebbe essere simile toohello seguente immagine:

    ![Creazione guidata nuovo gruppo di disponibilità: convalida](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Si verifica un avviso per la configurazione del listener hello poiché non è stato configurato un listener del gruppo di disponibilità. È possibile ignorare questo avviso perché in macchine virtuali di Azure crea listener hello dopo la creazione di bilanciamento del carico Azure hello.

10. In hello **riepilogo** pagina, fare clic su **fine**, quindi attendere la procedura guidata hello Configura hello nuovo gruppo di disponibilità. In hello **lo stato di avanzamento** pagina, è possibile fare clic su **ulteriori dettagli** tooview hello dettagliate lo stato di avanzamento. La procedura guidata hello termine, controllare hello **risultati** tooverify pagina che hello gruppo di disponibilità è stato creato correttamente.

     ![Creazione guidata nuovo gruppo di disponibilità: risultati](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Fare clic su **Chiudi** guidata hello tooexit.

### <a name="check-hello-availability-group"></a>Hello controllo gruppo di disponibilità

1. In **Esplora oggetti** espandere **Disponibilità elevata AlwaysOn**, quindi espandere **Gruppi di disponibilità**. Dovrebbe essere hello nuovo gruppo di disponibilità in questo contenitore. Fare doppio clic su hello gruppo di disponibilità e fare clic su **Mostra Dashboard**.

   ![Mostrare dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Il **AlwaysOn Dashboard** dovrebbe essere simile toothis.

   ![Dashboard gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   È possibile visualizzare le repliche hello, la modalità di failover di ogni stato di sincronizzazione di replica e hello hello.

2. In **Gestione cluster di failover** fare clic sul cluster. Selezionare **Ruoli**. Nome gruppo di disponibilità Hello utilizzato è un ruolo nel cluster hello. Tale gruppo di disponibilità non ha un indirizzo IP per le connessioni client, perché non è stato configurato un listener. Dopo aver creato un servizio di bilanciamento del carico di Azure, sarà necessario configurare il listener hello.

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Non tentare toofail su hello gruppo di disponibilità da hello gestione Cluster di Failover. È consigliabile eseguire tutte le operazioni di failover nel **Dashboard AlwaysOn** in SSMS. Per ulteriori informazioni, vedere [le restrizioni sull'utilizzo hello gestione Cluster di Failover con gruppi di disponibilità](https://msdn.microsoft.com/library/ff929171.aspx).
    >

A questo punto, è presente un gruppo di disponibilità con repliche in due istanze di SQL Server. È possibile spostare hello gruppo di disponibilità tra istanze. Non si dispone di un listener non è possibile connettersi ancora toohello gruppo di disponibilità. In macchine virtuali di Azure, il listener hello richiede un bilanciamento del carico. passaggio successivo Hello è bilanciamento del carico di hello toocreate in Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Creare un servizio di bilanciamento del carico di Azure

Nelle macchine virtuali di Azure un gruppo di disponibilità SQL Server richiede un servizio di bilanciamento del carico. servizio di bilanciamento del carico Hello contiene l'indirizzo IP hello per listener del gruppo di disponibilità di hello. Questa sezione vengono riepilogati come hello toocreate bilanciamento del carico in hello portale di Azure.

1. Nel portale di Azure hello, passare toohello gruppo di risorse in cui i computer SQL Server e fare clic su **+ Aggiungi**.
2. Cercare **Servizio di bilanciamento del carico**. Scegliere di bilanciamento del carico hello pubblicato da Microsoft.

   ![Gruppo di disponibilità in Gestione cluster di failover](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Fare clic su **Crea**.
3. Configurare i seguenti parametri di bilanciamento del carico hello hello.

   | Impostazione | Campo |
   | --- | --- |
   | **Nome** |Utilizzare un nome di bilanciamento del carico hello, ad esempio **sqlLB**. |
   | **Tipo** |Interno |
   | **Rete virtuale** |Utilizzare il nome di hello di hello rete virtuale di Azure. |
   | **Subnet** |Utilizza il nome di hello di subnet hello hello macchina virtuale è in.  |
   | **Assegnazione indirizzi IP** |Static |
   | **Indirizzo IP** |Usare un indirizzo disponibile nella subnet. |
   | **Sottoscrizione** |Utilizzare hello stessa sottoscrizione come macchina virtuale hello. |
   | **Posizione** |Utilizzare hello stesso percorso come macchina virtuale hello. |

   portale di Azure-blade Hello dovrebbe essere simile al seguente:

   ![Crea servizio di bilanciamento del carico](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Fare clic su **crea**, servizio di bilanciamento del carico toocreate hello.

servizio di bilanciamento del carico hello tooconfigure occorre toocreate un pool back-end, un probe e regole di bilanciamento del carico di set hello. Eseguire le operazioni seguenti nel portale di Azure hello.

### <a name="add-backend-pool"></a>Aggiungere un pool back-end

1. Nel portale di Azure hello, passare tooyour gruppo di disponibilità. Potrebbe essere necessario bilanciamento del carico di toorefresh hello vista toosee hello appena creato.

   ![Trovare il servizio di bilanciamento del carico nel gruppo di risorse](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Fare clic su servizio di bilanciamento del carico hello, fare clic su **pool back-end**, fare clic su **+ Aggiungi**. Impostare il pool di back-end hello come segue:

   | Impostazione | Descrizione | Esempio
   | --- | --- |---
   | **Nome** | Digitare un nome in formato testo | SQLLBBE
   | **Associato a** | Selezionare dall'elenco | Set di disponibilità
   | **Set di disponibilità** | Utilizzare un nome del gruppo di disponibilità hello che si trovano le macchine virtuali di SQL Server in | sqlAvailabilitySet |
   | **Macchine virtuali** |Hello due nomi di macchina virtuale di Azure SQL Server | sqlserver-0, sqlserver-1

1. Digitare il nome di hello per pool back-end hello.

1. Fare clic su **+ Aggiungi una macchina virtuale**.

1. Per i set di disponibilità hello, scegliere disponibilità hello impostare tale hello presenti istanze di SQL Server.

1. Per le macchine virtuali, inclusi sia di hello istanze di SQL Server. Non includere server di controllo di condivisione file hello.

1. Fare clic su **OK** pool back-end di toocreate hello.

### <a name="set-hello-probe"></a>Set hello probe

1. Fare clic su servizio di bilanciamento del carico hello, fare clic su **probe di integrità**, fare clic su **+ Aggiungi**.

1. Impostare i probe di integrità hello come segue:

   | Impostazione | Descrizione | Esempio
   | --- | --- |---
   | **Nome** | Text | SQLAlwaysOnEndPointProbe |
   | **Protocollo** | Scegliere TCP | TCP |
   | **Porta** | Qualsiasi porta non usata | 59999 |
   | **Interval**  | Hello tempo tra probe tentativi espresso in secondi |5 |
   | **Soglia non integra** | numero di errori di probe consecutivi che devono verificarsi per una macchina virtuale di toobe considerato non integro Hello  | 2 |

1. Fare clic su **OK** tooset probe di integrità hello.

### <a name="set-hello-load-balancing-rules"></a>Impostare regole di bilanciamento del carico di hello

1. Fare clic su servizio di bilanciamento del carico hello, fare clic su **regole di bilanciamento del carico**, fare clic su **+ Aggiungi**.

1. Impostare hello bilanciamento del carico regole come indicato di seguito.
   | Impostazione | Descrizione | Esempio
   | --- | --- |---
   | **Nome** | Text | SQLAlwaysOnEndPointListener |
   | **Indirizzo IP front-end IP** | Scegliere un indirizzo |Usa indirizzo hello creato al momento della creazione del bilanciamento del carico hello. |
   | **Protocollo** | Scegliere TCP |TCP |
   | **Porta** | Utilizzare la porta hello hello istanza di SQL Server | 1433 |
   | **Porta back-end** | Questo campo non viene usato quando l'indirizzo IP mobile è impostato per Direct Server Return | 1433 |
   | **Probe** |nome Hello specificato per il probe hello | SQLAlwaysOnEndPointProbe |
   | **Persistenza della sessione** | Elenco a discesa | **Nessuno** |
   | **Timeout di inattività** | Minuti tookeep aprire una connessione TCP | 4 |
   | **IP mobile (Direct Server Return)** | |Enabled |

   > [!WARNING]
   > Direct Server Return viene impostato durante la creazione. Non può essere modificato.

1. Fare clic su **OK** tooset hello bilanciamento del carico regole.

## <a name="configure-listener"></a>Configurare il listener hello

Hello Avanti cosa toodo è tooconfigure un listener del gruppo di disponibilità nel cluster di failover hello.

> [!NOTE]
> Questa esercitazione viene illustrato come un listener single - con un IP ILB toocreate indirizzo. toocreate uno o più listener utilizzando uno o più indirizzi IP, vedere [listener Crea gruppo di disponibilità e bilanciamento del carico | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Impostare la porta del listener

In SQL Server Management Studio, impostare la porta di attesa hello.

1. Avviare SQL Server Management Studio e connettersi toohello la replica primaria.

1. Passare troppo**disponibilità elevata AlwaysOn** | **gruppi di disponibilità** | **listener del gruppo di disponibilità**.

1. Viene visualizzato il nome del listener hello creati in Gestione Cluster di Failover. Il nome del listener hello destro e fare clic su **proprietà**.

1. In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzato in precedenza (1433 è predefinito hello), quindi fare clic su **OK**.

Ora si ha un gruppo di disponibilità di SQL Server nelle macchine virtuali di Azure in esecuzione in modalità Resource Manager.

## <a name="test-connection-toolistener"></a>Test connessione toolistener

connessione hello tootest:

1. RDP tooa SQL Server in hello stesso virtuale di rete, ma non non replica hello personalizzati. È possibile utilizzare altri Server SQL cluster hello hello.

1. Utilizzare **sqlcmd** connessione hello tootest di utilità. Ad esempio, lo script seguente hello stabilisce un **sqlcmd** replica primaria toohello di connessione tramite il listener hello con l'autenticazione di Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Se il listener di hello utilizza una porta diversa da hello predefinita (1433) di porta, specificare la porta hello nella stringa di connessione hello. Ad esempio, hello comando sqlcmd riportato di seguito si connette tooa listener a porta 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

connessione SQLCMD Hello si connette automaticamente toowhichever istanza di SQL Server ospitata hello la replica primaria.

> [!TIP]
> Assicurarsi che sia aperta nel firewall hello di entrambi i server SQL porta hello specificata. Entrambi i server richiedono una regola in ingresso per hello la porta TCP in uso. Per altre informazioni, vedere [Aggiungere o modificare una regola del firewall](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Passaggi successivi

- [Aggiungere un bilanciamento del carico IP indirizzo tooa per un gruppo di disponibilità secondo](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
