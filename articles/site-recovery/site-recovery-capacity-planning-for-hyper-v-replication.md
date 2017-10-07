---
title: "strumento di pianificazione della capacità hello Hyper-V aaaRun per il ripristino del sito | Documenti Microsoft"
description: "In questo articolo viene descritto come toorun hello dello strumento di pianificazione della capacità di Hyper-V per Azure Site Recovery"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Eseguire lo strumento di pianificazione della capacità di hello Hyper-V per il ripristino del sito

Come parte della distribuzione di Azure Site Recovery, è necessario toofigure out ai requisiti di larghezza di banda e di replica. strumento di pianificazione della capacità di Hello Hyper-V per il ripristino del sito consente si toodo, per la replica della macchina virtuale Hyper-V.

In questo articolo viene descritto come toorun hello dello strumento di pianificazione della capacità di Hyper-V. Questo strumento deve essere utilizzato insieme a informazioni di hello in [pianificazione della capacità per il ripristino del sito](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Prima di iniziare
Eseguire lo strumento hello in un nodo di server o cluster Hyper-V nel sito primario. server host Hyper-V di toorun hello strumento hello deve:

* Sistema operativo: Windows Server 2012 o 2012 R2
* Memoria: 20 MB (minimo)
* CPU: sovraccarico del 5% (minimo)
* Spazio su disco: 5 MB (minimo)

Prima di eseguire lo strumento di hello, è necessario tooprepare hello primario di sito. Se si esegue la replica tra due siti locali e si desidera toocheck della larghezza di banda, è necessario tooprepare anche un server di replica.

## <a name="step-1-prepare-hello-primary-site"></a>Passaggio 1: Preparare il sito primario di hello

1. Nel sito primario di hello, rendere un elenco di tutte le macchine virtuali Hyper-V si desidera hello tooreplicate e hello in cui si trovano gli host Hyper-V o i cluster. strumento Hello è possibile eseguire per più host autonomo o per un singolo cluster, ma non entrambi contemporaneamente. È inoltre necessario toorun separatamente per ogni sistema operativo, in modo da raccogliere informazioni sui server Hyper-V come indicato di seguito:

   * Server autonomi Windows Server 2012
   * Cluster Windows Server 2012
   * Server autonomi Windows Server 2012 R2
   * Cluster Windows Server 2012 R2
2. Abilitare accesso remoto tooWMI in tutti gli host Hyper-V hello e cluster. Eseguire questo comando in ogni server o cluster, vengono impostate le regole del firewall che toomake e le autorizzazioni utente:

        netsh firewall set service RemoteAdmin enable
3. Abilitare il monitoraggio delle prestazioni su server e cluster, come indicato di seguito:

   * Hello aprire Windows Firewall con hello **sicurezza avanzata** snap-in, e quindi regole connessioni in entrata seguente hello Abilita: **accesso alla rete COM+ (DCOM-IN)** e tutte le regole di hello **remota registro eventi Gruppo di gestione**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Passaggio 2: Preparare un server di replica (replica tooon tra più sedi locali)
Non è necessario toodo questa se si esegue la replica tooAzure.

È consigliabile configurare un singolo host Hyper-V come un server di ripristino, in modo che una macchina virtuale di fittizia può essere replicata tooit toocheck larghezza di banda.  È possibile ignorare questo passaggio, ma non sarà in grado di toomeasure della larghezza di banda a meno che non è eseguire questa operazione.

1. Se si desidera toouse un nodo del cluster come replica hello configurare gestore di Replica Hyper-V:

   * In **Server Manager** aprire **Gestione cluster di Failover**.
   * Connettere il cluster toohello, evidenziare il nome del cluster hello e fare clic su **azioni** > **Configura ruolo** tooopen configurazione guidata disponibilità elevata di hello.
   * In **Selezione ruolo** fare clic su **Gestore di replica Hyper-V**. Nella procedura guidata hello forniscono un **nome NetBIOS** hello e **indirizzo IP** toobe utilizzato come hello connessione punto toohello cluster (detto punto di accesso client). Hello **gestore Replica Hyper-V** verranno configurati, risultante in un nome di punto di accesso client che si noti.
   * Verificare il ruolo gestore di Replica Hyper-V hello impostato come online e può eseguire il failover tra tutti i nodi del cluster di hello. toodo, fare clic con il pulsante destro ruolo hello, scegliere troppo**spostare**, quindi fare clic su **Seleziona nodo**. Selezionare un nodo e quindi fare clic su **OK**.
   * Se si utilizza l'autenticazione basata su certificato, assicurarsi che ogni nodo del cluster e punto di accesso client hello tutti installato hello certificato.
2. Abilitare un server di replica:

   * Per un cluster aprire Gestione Cluster di errore, connettere il cluster toohello e fare clic su **ruoli** > ruolo Seleziona > **le impostazioni di replica** > **abilita questo cluster come una Replica server**. Se si utilizza un cluster come replica hello, è necessario il ruolo gestore di Replica Hyper-V di hello toohave è presente nel cluster hello nel sito primario come hello.
   * Per un server autonomo, aprire la Console di gestione di Hyper-V. In hello **azioni** riquadro, fare clic su **impostazioni Hyper-V** per server hello desiderato tooenable e in **configurazione della replica** fare clic su **abilitare questa opzione computer come server di Replica**.
3. Configurare l'autenticazione:

   * In **autenticazione e porte**, selezionare la modalità tooauthenticate hello server primario e porte di autenticazione hello. Se si utilizza un certificato di clic **Seleziona certificato** tooselect uno. Se gli host di Hyper-V primario e di ripristino hello hello utilizza Kerberos, nello stesso dominio o in domini trusted. Usare i certificati per domini diversi o la distribuzione in un gruppo di lavoro.
   * In **autorizzazione e l'archiviazione**, consentire **qualsiasi** autenticazione con il server di replica toothis server (primario) toosend replica dei dati.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Eseguire **netsh http show servicestate**, toocheck listener hello è in esecuzione per hello protocollo/porta specificata:  
4. Configurare i firewall. Durante l'installazione di Hyper-V, le regole del firewall vengono create tooallow traffico sulle porte predefinite di hello (HTTPS su 443, Kerberos su 80). Abilitare queste regole come indicato di seguito:
  - Autenticazione del certificato in un cluster (443): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Autenticazione Kerberos nel cluster (80): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Autenticazione del certificato in un server autonomo: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Autenticazione Kerberos in un server autonomo: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Passaggio 3: Eseguire lo strumento di pianificazione della capacità di hello
Dopo aver preparato il sito primario e configurare un server di ripristino, è possibile eseguire lo strumento hello.

1. [Scaricare](https://www.microsoft.com/download/details.aspx?id=39057) strumento hello hello Microsoft Download Center.
2. Eseguire lo strumento hello da uno dei server primari hello (o uno dei nodi di hello dal cluster primario hello). Fare clic sul file .exe hello e quindi scegliere **Esegui come amministratore**.
3. In **prima di iniziare**, specificare per quanto tempo toocollect dati. È consigliabile che eseguire lo strumento hello durante tooensure ore di produzione che dati siano rappresentativo. Se si sta solo tentando toovalidate connettività di rete, è possibile raccogliere solo un minuto.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. In **i dettagli del sito primario**, specificare il nome di server hello o un FQDN per un host autonomo o per un cluster di specificare il FQDN del client hello hello accettare punto, il nome del cluster o un qualsiasi nodo cluster hello e quindi fare clic su **Avanti**. strumento Hello rileva automaticamente il nome di hello del server di hello in cui viene eseguito. strumento Hello preleva le macchine virtuali che possono essere monitorate per hello server specificati.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. In **i dettagli del sito di Replica**, se esegue la replica tooAzure oppure se si esegue la replica Data Center secondario tooa e non è ancora configurato un server di replica, selezionare **ignorare test che includono il sito di replica**. Se si replicano Data Center secondario tooa e aver configurato un tipo di replica, immettere nome FQDN del server autonomo hello o il punto di accesso client hello per cluster hello in **nome (o Server) Hyper-V Replica Broker estremità**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. In **dettagli della Replica estesa**, abilitare **hello Ignora verifica del sito di Replica estesa che coinvolgono**. Questi test non sono supportati da Site Recovery.
7. In **scegliere le macchine virtuali tooReplicate**, strumenti di hello connette toohello server o cluster e visualizza le macchine virtuali e dischi in esecuzione nel server primario hello, in base alle impostazioni di hello specificato sulla hello **i dettagli del sito primario**  pagina. Le VM già abilitate per la replica o non in esecuzione non verranno visualizzate. Selezionare le macchine virtuali hello per cui si desidera toocollect metriche. Selezione dischi rigidi virtuali hello automaticamente raccoglie troppo dati hello macchine virtuali.
8. Se è stato configurato un server di replica o di un cluster in **informazioni di rete**, specificare hello approssimativo larghezza di banda WAN si ritiene che verrà usata tra siti primaria e replica di hello e certificati hello selezionare se si è configurato autenticazione del certificato.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. In **riepilogo**, controllare le impostazioni di hello e fare clic su **Avanti** toobegin raccolta delle metriche. Lo stato di avanzamento dello strumento e lo stato viene visualizzato sulla hello **calcolare capacità** pagina. Al termine dell'esecuzione dello strumento hello, fare clic su **Visualizza Report** tooview output di hello. Per impostazione predefinita, i report e i log vengono archiviati in **%systemdrive%\Users\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Passaggio 4: Interpretare i risultati di hello

Di seguito sono metriche importanti hello. È possibile ignorare le metriche non elencate qui. Non sono rilevanti per Site Recovery.

### <a name="on-premises-tooon-premises-replication"></a>Replica tooon tra più sedi locali

* Impatto della replica nel calcolo dell'host primario hello, memoria
* Impatto della replica hello primario, spazio su disco di archiviazione dell'host di ripristino, IOPS
* Larghezza di banda totale necessaria per la replica delta (Mbps)
* Larghezza di banda di rete osservato tra host primario hello e host di ripristino hello (Mbps)
* Suggerimento per il numero ideale di hello di trasferimenti paralleli attivi tra hello due host/cluster

### <a name="on-premises-tooazure-replication"></a>Replica locale tooAzure

* Impatto della replica nel calcolo dell'host primario hello, memoria
* Impatto della replica archiviazione lo spazio dell'host primario hello su disco, IOPS
* Larghezza di banda totale necessaria per la replica delta (Mbps)

## <a name="more-resources"></a>Altre risorse
* Per informazioni dettagliate sullo strumento hello, leggere il documento hello che accompagna il download dello strumento hello.
* Guardare un procedura dettagliata dello strumento hello in Keith Mayer [blog TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Ottenere i risultati di hello](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) il test delle prestazioni per la replica Hyper-V tooon tra più sedi locali

## <a name="next-steps"></a>Passaggi successivi

Dopo aver completato la pianificazione della capacità, iniziare la distribuzione di Site Recovery:

* [Replicare macchine virtuali Hyper-V in VMM cloud tooAzure](site-recovery-vmm-to-azure.md)
* [Replicare le macchine virtuali Hyper-V (senza VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Eseguire la replica di VM Hyper-V tra siti VMM](site-recovery-vmm-to-vmm.md)
