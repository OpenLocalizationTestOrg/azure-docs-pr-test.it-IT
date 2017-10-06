---
title: aaaSet un applicazioni MPI di RDMA Windows cluster toorun | Documenti Microsoft
description: Informazioni su come un cluster Windows HPC Pack con dimensioni H16r, H16mr, A8 o A9 VM toouse toocreate hello App MPI toorun di rete RDMA di Azure.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Configurare un cluster di Windows RDMA con applicazioni MPI toorun di HPC Pack
Configurare un cluster di Windows RDMA in Azure con [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) e [dimensioni delle macchine Virtuali di calcolo ad alte prestazioni](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun le applicazioni parallele interfaccia MPI (Message Passing). Quando si configurano nodi con supporto per RDMA e basati su Windows Server in un cluster HPC Pack, le applicazioni MPI comunicano in modo efficiente tramite una rete a bassa latenza e a velocità effettiva elevata in Azure, sulla base della tecnologia di accesso diretto a memoria remota (RDMA).

Se si desidera toorun carichi di lavoro MPI nelle macchine virtuali Linux tale accesso hello rete RDMA di Azure, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Opzioni di distribuzione del cluster HPC Pack
Microsoft HPC Pack è uno strumento fornito in toocreate alcun costo aggiuntivo HPC cluster locale o in Azure toorun Windows o applicazioni Linux HPC. HPC Pack include un ambiente di runtime per l'implementazione Microsoft hello hello messaggio passando interfaccia per Windows (MS-MPI). Se utilizzato con il supporto per RDMA istanze in esecuzione un sistema operativo Windows Server supportato, HPC Pack fornisce le applicazioni MPI Windows toorun un'opzione efficiente tale accesso hello rete RDMA di Azure. 

In questo articolo vengono descritti due scenari e i collegamenti toodetailed indicazioni tooset di un cluster di Windows RDMA con Microsoft HPC Pack. 

* Scenario 1. Distribuzione di istanze del ruolo di lavoro a elevato utilizzo di calcolo (PaaS)
* Scenario 2. Distribuzione di nodi di calcolo in macchine virtuali a elevato utilizzo di calcolo (IaaS)

Per le istanze con utilizzo intensivo di calcolo di toouse prerequisiti generali con Windows, vedere [dimensioni delle macchine Virtuali di calcolo ad alte prestazioni](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Scenario 1: Distribuzione di istanze del ruolo di lavoro a elevato utilizzo di calcolo (PaaS)
Da un cluster HPC Pack esistente, aggiungere risorse di calcolo aggiuntive sotto forma di istanze del ruolo di lavoro di Azure (nodi di Azure) in esecuzione in un servizio cloud (PaaS). Questa funzionalità, denominata anche "potenziamento tooAzure" da HPC Pack, supporta una gamma di dimensioni per le istanze del ruolo worker hello. Quando aggiunta hello nodi di Azure, specificare uno dei formati di hello con supporto per RDMA.

Di seguito sono indicazioni e procedure tooburst in grado di supportare tooRDMA istanze di Azure da un oggetto esistente (in genere locale) cluster. Utilizzare simile procedure tooadd lavoro ruolo istanze tooan HPC Pack nodo head distribuito in una macchina virtuale di Azure.

> [!NOTE]
> Per un'esercitazione tooburst tooAzure con HPC Pack, vedere [configurazione di un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Considerare di hello in passaggi applicati in modo specifico i nodi di Azure in grado di supportare tooRDMA hello.
> 
> 

![Potenziamento tooAzure][burst]

### <a name="steps"></a>Passi
1. **Distribuire e configurare un nodo head HPC Pack 2012 R2**
   
    Scaricare il pacchetto di installazione hello più recente HPC Pack da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Per requisiti e le istruzioni tooprepare per una distribuzione di potenziamento in Azure, vedere [potenziamento tooAzure istanze di lavoro con Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).
2. **Configurare un certificato di gestione nella sottoscrizione di Azure hello**
   
    Configurare una connessione di hello certificato toosecure tra Azure e hello del nodo head. Per le opzioni e procedure, vedere [hello tooConfigure scenari il certificato di gestione di Azure per HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). Per le distribuzioni di test, HPC Pack installa predefinito Microsoft HPC Azure certificato di gestione è possibile caricare rapidamente tooyour sottoscrizione di Azure.
3. **Creare un nuovo servizio cloud e un account di archiviazione**
   
    Utilizzare un servizio cloud e un account di archiviazione hello toocreate portale Azure per la distribuzione di hello in un'area in cui sono disponibili istanze hello con supporto per RDMA.
4. **Creare un modello di nodo di Azure**
   
    Utilizzare Creazione guidata modello di nodo hello in Gestione Cluster HPC. Per istruzioni, vedere [creare un modello di nodo di Azure](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) in "Passaggi tooDeploy nodi di Azure con Microsoft HPC Pack".
   
    Per i test iniziali, è consigliabile configurare i criteri di disponibilità manuali nel modello di hello.
5. **Aggiungere nodi toohello cluster**
   
    Utilizzare Aggiunta guidata nodi hello in Gestione Cluster HPC. Per ulteriori informazioni, vedere [toohello aggiungere nodi di Azure Cluster HPC Windows](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Quando si specificano dimensioni hello dei nodi di hello, selezionare una delle dimensioni di istanza che supportano RDMA hello.
   
   > [!NOTE]
   > In ogni distribuzione di potenziamento tooAzure con le istanze con utilizzo intensivo di calcolo hello HPC Pack distribuisce automaticamente almeno due istanze di supporto per RDMA (ad esempio A8) come nodi proxy, inoltre le istanze del ruolo di lavoro di Azure toohello specificate. nodi di Hello proxy utilizzano core allocati toohello sottoscrizione e comportano un addebito insieme alle istanze del ruolo di lavoro di Azure hello.
   > 
   > 
6. **Avviare i nodi di hello (provisioning) e portarli online toorun processi**
   
    Selezionare i nodi di hello e utilizzare hello **avviare** azione in Gestione Cluster HPC. Al termine il provisioning, selezionare i nodi di hello e utilizzare hello **in linea** azione in Gestione Cluster HPC. i nodi di Hello sono processi toorun pronto.
7. **Inviare cluster toohello processi**
   
   Utilizzare i processi di HPC Pack processo invio strumenti toorun cluster. Vedere l'argomento relativo alla [gestione dei processi con Microsoft HPC Pack](http://technet.microsoft.com/library/jj899585.aspx).
8. **Arresta nodi di hello (effettuarne il deprovisioning)**
   
   Al termine dei processi in esecuzione, portare offline i nodi di hello e utilizzare hello **arrestare** azione in Gestione Cluster HPC.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Scenario 2: Distribuzione di nodi di calcolo in macchine virtuali a elevato utilizzo di calcolo (IaaS)
In questo scenario, si distribuisce nodo head di HPC Pack hello e nodi di calcolo al cluster in macchine virtuali in una rete virtuale di Azure. HPC Pack fornisce una serie di [opzioni di distribuzione nelle macchine virtuali di Azure](../../linux/hpcpack-cluster-options.md), inclusi script di distribuzione automatizzati e modelli di avvio rapido di Azure. Ad esempio, hello seguenti considerazioni e i passaggi per hello toouse [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) per automatizzare la distribuzione di hello di un cluster HPC Pack 2012 R2 in Azure.

![Cluster in macchine virtuali di Azure][iaas]

### <a name="steps"></a>Passi
1. **Creare un nodo head del cluster e macchine virtuali del nodo di calcolo eseguendo lo script di distribuzione IaaS di HPC Pack hello in un computer client**
   
    Scaricare il pacchetto di Script di distribuzione IaaS di HPC Pack hello dal hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    tooprepare hello client computer, creare file di configurazione dello script hello e hello esecuzione script, vedere [creare un Cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](hpcpack-cluster-powershell-script.md). 
   
    nodi di calcolo toodeploy con supporto per RDMA, hello nota considerazioni aggiuntive seguenti:
   
   * **Rete virtuale**: specificare una nuova rete virtuale in un'area in cui hello con supporto per RDMA dimensioni dell'istanza desiderata toouse è disponibile.
   * **Sistema operativo Windows Server**: toosupport connettività RDMA, specificare un sistema operativo Windows Server 2012 R2 o Windows Server 2012 per il nodo di calcolo hello macchine virtuali.
   * **Servizi cloud**: è consigliabile eseguire la distribuzione del nodo head in un servizio cloud e dei nodi di calcolo in un altro servizio cloud.
   * **Dimensione del nodo head**: per questo scenario, considerare una dimensione di almeno A4 (molto grande) per il nodo head hello.
   * **Estensione HpcVmDrivers**: hello script di distribuzione installa agente VM di Azure hello e hello estensione HpcVmDrivers automaticamente quando si distribuiscono i nodi di calcolo A8 o A9 di dimensioni con un sistema operativo Windows Server. HpcVmDrivers installa driver nelle macchine virtuali del nodo di calcolo hello in modo da potersi connettere toohello di rete RDMA. Nelle macchine virtuali serie H con supporto per RDMA, è necessario installare manualmente l'estensione HpcVmDrivers hello. Vedere [Dimensioni delle VM High Performance Computing (HPC)](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Configurazione della rete cluster**: script di distribuzione hello imposta automaticamente il cluster HPC Pack hello nella topologia 5 (tutti i nodi nella rete aziendale hello). Questa topologia è obbligatoria per tutte le distribuzioni di cluster HPC Pack nelle VM. Non modificare topologia di rete cluster hello in un secondo momento.
2. **Portare i nodi di calcolo hello processi toorun online**
   
    Selezionare i nodi di hello e utilizzare hello **in linea** azione in Gestione Cluster HPC. i nodi di Hello sono processi toorun pronto.
3. **Inviare cluster toohello processi**
   
    La connessione di processi di toosubmit toohello nodo head o di impostare un toodo del computer locale questo. Per informazioni, vedere [tooan inviare processi HPC cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **I nodi di hello Take offline e interrompere (deallocarle)**
   
    Al termine dei processi in esecuzione, portare offline i nodi di hello in Gestione Cluster HPC. Utilizzare quindi tooshut strumenti di gestione di Azure loro verso il basso.

## <a name="run-mpi-applications-on-hello-cluster"></a>Eseguire applicazioni MPI nel cluster hello
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Esempio: Eseguire mpipingpong su un cluster HPC Pack
tooverify di istanze di hello con supporto per RDMA, eseguire una distribuzione di HPC Pack hello HPC Pack **mpipingpong** comando cluster hello. **MPIPingPong** invia pacchetti di dati tra nodi associati ripetutamente toocalculate le misure relative alla latenza e velocità effettiva e le statistiche di rete abilitate per RDMA applicazione hello. Questo esempio viene illustrato un modello tipico per l'esecuzione di un processo MPI (in questo caso, **mpipingpong**) utilizzando cluster hello **mpiexec** comando.

Questo esempio si presuppone aggiunti nodi di Azure in una configurazione "potenziamento tooAzure" ([lo Scenario 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Se HPC Pack è stato distribuito in un cluster di macchine virtuali di Azure, si sarà necessario toomodify hello comando sintassi toospecify un altro gruppo di nodi e ambiente aggiuntive variabili toodirect traffico toohello RDMA rete.

toorun mpipingpong sul cluster hello:

1. Nel nodo head hello o in un computer client configurato correttamente, aprire un prompt dei comandi.
2. tooestimate latenza tra coppie di nodi in una distribuzione di potenziamento in Azure di quattro nodi, hello tipo successivo comando toosubmit mpipingpong di toorun un processo con un pacchetto di piccole dimensioni e il numero di iterazioni:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    comando Hello restituisce hello ID di processo hello viene inviato.
   
    Se è stato distribuito il cluster di HPC Pack hello distribuito in macchine virtuali di Azure, specificare un gruppo di nodi contenente distribuite in un singolo servizio cloud macchine virtuali del nodo di calcolo e modificare hello **mpiexec** comando come segue:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Al termine del processo di hello, hello tooview output (in questo caso, output di hello dell'attività 1 del processo di hello), hello tipo seguente
   
    ```Command
    task view <JobID>.1
    ```
   
    dove &lt; *JobID* &gt; ID hello hello del processo di cui è stata inviata.
   
    output di Hello include seguenti di toohello latenza risultati simili.
   
    ![Latenza ping pong][pingpong1]
4. i nodi di potenziamento tooestimate velocità effettiva tra coppie di Azure, digitare quanto segue di hello comando toosubmit toorun un processo **mpipingpong** con pacchetti di grandi dimensioni e alcune iterazioni:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    comando Hello restituisce hello ID di processo hello viene inviato.
   
    In un cluster HPC Pack distribuito in macchine virtuali di Azure, modificare il comando hello come indicato nel passaggio 2.
5. Al termine del processo di hello, hello tooview output (in questo caso, output di hello dell'attività 1 del processo di hello), hello tipo seguente:
   
    ```Command
    task view <JobID>.1
    ```
   
   output di Hello include seguente toohello simile di velocità effettiva dei risultati.
   
   ![Velocità effettiva ping pong][pingpong2]

### <a name="mpi-application-considerations"></a>Considerazioni sulle applicazioni MPI
Di seguito sono riportate alcune considerazioni riguardanti l'esecuzione di applicazioni MPI con HPC Pack in Azure. Alcuni si applicano solo toodeployments di nodi di Azure (istanze del ruolo di lavoro aggiunte in una configurazione "potenziamento tooAzure").

* Le istanze del ruolo di lavoro in un servizio cloud vengono sottoposte periodicamente a nuovo provisioning senza preavviso da Azure, ad esempio per la manutenzione del sistema o in caso di errore di un'istanza. Se un'istanza reprovisioning mentre è in esecuzione un processo MPI, istanza hello perde i dati e restituisce lo stato toohello quando prima distribuzione, che possono causare toofail processo MPI di hello. Hello più nodi che si utilizza per un singolo processo MPI e hello più hello processo viene eseguito, hello più probabile che una delle istanze di hello reprovisioning mentre è in esecuzione un processo. Considerare questo aspetto anche se si definisce un singolo nodo nella distribuzione hello come file server.
* toorun i processi MPI in Azure, non sono istanze di toouse hello con supporto per RDMA. È possibile usare qualsiasi dimensione di istanza supportata da HPC Pack. Tuttavia, le istanze che supportano RDMA hello sono consigliate per l'esecuzione di processi MPI su scala relativamente grande che sono sensibili toohello latenza e larghezza di banda di hello della rete hello che connette i nodi di hello. Se si utilizzano gli altri processi MPI dimensioni toorun distinzione di larghezza di banda e di latenza, è consigliabile eseguire piccoli processi in cui una singola attività viene eseguita solo alcuni nodi.
* Le istanze di tooAzure applicazioni distribuite sono soggetto toohello associate a un'applicazione hello condizioni di licenza. Contattare il fornitore hello di qualsiasi applicazione commerciale per le licenze o altre restrizioni per l'esecuzione nel cloud hello. Non tutti i fornitori offrono licenze con pagamento in base al consumo.
* Server licenze, condivisioni e nodi locali tooaccess, necessario configurare ulteriori istanze di Azure. Ad esempio, hello tooenable tooaccess nodi di Azure un server licenze locale, è possibile configurare una rete virtuale di Azure da sito a sito.
* toorun di applicazioni MPI in istanze di Azure, registrare ogni applicazione MPI con Windows Firewall nelle istanze di hello eseguendo hello **hpcfwutil** comando. In questo modo sul posto di tootake le comunicazioni MPI su una porta assegnata dinamicamente dal firewall hello.
  
  > [!NOTE]
  > Per le distribuzioni di potenziamento tooAzure, è anche possibile configurare un toorun di comando di eccezione firewall automaticamente in tutti i nuovi nodi di Azure che vengono aggiunti tooyour cluster. Dopo aver eseguito hello **hpcfwutil** comando e verificare che il corretto funzionamento, aggiungere hello comando tooa lo script di avvio per i nodi di Azure. Per ulteriori informazioni, vedere l'articolo relativo a come [usare uno script di avvio per i nodi di Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack Usa hello CCP_MPI_NETMASK cluster ambiente variabile toospecify un intervallo di indirizzi validi per la comunicazione MPI. A partire da HPC Pack 2012 R2, variabile di ambiente cluster CCP_MPI_NETMASK hello interessa solo la comunicazione MPI tra nodi di calcolo cluster appartenenti a un dominio (in locale o in macchine virtuali di Azure). variabile di Hello viene ignorata dai nodi aggiunti in una configurazione di potenziamento tooAzure.
* I processi MPI non eseguiti in istanze di Azure distribuite in diversi servizi cloud (ad esempio, nelle distribuzioni di potenziamento tooAzure con modelli di nodo diversi o nodi di calcolo di Azure VM distribuiti in più servizi cloud). Se si dispone di più distribuzioni di nodi di Azure avviate con modelli di nodo diversi, è necessario eseguire processi MPI hello in un solo set di nodi di Azure.
* Quando si aggiungere nodi di Azure tooyour cluster e portarli online, hello servizio Utilità di pianificazione processi HPC immediatamente tenta toostart processi nei nodi hello. Se solo una parte del carico di lavoro può eseguire in Azure, assicurarsi di aggiornare o creare toodefine di modelli di processo il processo di tipi è possono eseguire in Azure. Ad esempio, tooensure che i processi inviati con un modello di processo viene eseguito solo nei nodi di Azure, aggiungere modello di processo toohello proprietà nodo gruppi hello e selezionare AzureNodes come hello valore obbligatorio. toocreate gruppi personalizzati per i nodi di Azure, utilizzare i cmdlet Add-HpcGroup HPC PowerShell hello.

## <a name="next-steps"></a>Passaggi successivi
* Come un'alternativa toousing HPC Pack, sviluppare con hello Azure Batch servizio toorun applicazioni MPI in pool gestiti di nodi di calcolo di Azure. Vedere [multi-istanza usare attività toorun applicazioni di interfaccia MPI (Message Passing) in Azure Batch](../../../batch/batch-mpi.md).
* Se si desidera toorun Linux MPI applicazioni che accedono hello rete RDMA di Azure, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
