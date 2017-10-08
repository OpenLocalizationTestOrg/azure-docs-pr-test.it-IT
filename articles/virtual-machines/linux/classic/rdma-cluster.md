---
title: aaaSet un applicazioni MPI di Linux RDMA cluster toorun | Documenti Microsoft
description: Creare un cluster Linux di toouse H16r, H16mr, A8 o A9 VM di dimensioni hello Azure RDMA rete toorun MPI App
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Impostare un applicazioni MPI toorun di Linux RDMA cluster
Informazioni su come tooset backup un RDMA Linux cluster in Azure con [dimensioni delle macchine Virtuali di calcolo ad alte prestazioni](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun le applicazioni parallele interfaccia MPI (Message Passing). Questo articolo fornisce passaggi tooprepare un toorun immagine HPC Linux MPI Intel in un cluster. Dopo la preparazione, si distribuisce un cluster di macchine virtuali usando questa immagine di dimensioni di macchina virtuale di Azure che supportano RDMA hello (attualmente H16r, H16mr, A8 o A9). Utilizzare le applicazioni MPI toorun di cluster hello che comunicano in modo efficiente su una rete a bassa latenza, velocità effettiva elevata, basata sulla tecnologia di diretto a memoria remota (RDMA) di accesso.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="cluster-deployment-options"></a>Opzioni di distribuzione del cluster
Di seguito sono metodi è possibile usare un cluster Linux RDMA toocreate con o senza un'utilità di pianificazione del processo.

* **Script di Azure CLI**: come illustrato più avanti in questo articolo, utilizzare hello [interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) distribuzione di hello tooscript (CLI) di un cluster di macchine virtuali che supportano RDMA. Hello CLI in modalità di gestione del servizio crea hello i nodi del cluster in modo seriale nel modello di distribuzione classica hello, per consentire la distribuzione di molti nodi di calcolo potrebbe richiedere alcuni minuti. hello tooenable connessione di rete RDMA quando si utilizza il modello di distribuzione classica hello, distribuire le macchine virtuali hello in hello stesso servizio cloud.
* **Modelli di Azure Resource Manager**: È anche possibile usare toodeploy modello di distribuzione di gestione delle risorse hello un cluster di macchine virtuali con supporto per RDMA che si connette rete RDMA toohello. È possibile [Crea modello personale](../../../resource-group-authoring-templates.md), o controllare hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) per i modelli forniti da Microsoft o hello community toodeploy hello soluzione desiderata. Modelli di gestione risorse possono fornire un modo rapido e affidabile di toodeploy un cluster Linux. hello tooenable connessione di rete RDMA quando si Usa modello di distribuzione di gestione risorse hello, distribuire le macchine virtuali di hello in hello stesso set di disponibilità.
* **HPC Pack**: creare un cluster di Microsoft HPC Pack in Azure e aggiungere il supporto per RDMA nodi di calcolo che eseguono una rete RDMA di supportata di Linux distribuzione tooaccess hello. Per ulteriori informazioni, vedere [Introduzione all’uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>I passaggi di distribuzione di esempio nel modello classico hello
Hello passaggi seguenti mostrano come personalizzarlo, toouse hello Azure CLI toodeploy una VM di HPC SUSE Linux Enterprise Server (SLES) 12 SP1 da Azure Marketplace, hello e creare un'immagine di macchina virtuale personalizzata. È quindi possibile utilizzare hello immagine tooscript hello la distribuzione di un cluster di macchine virtuali che supportano RDMA.

> [!TIP]
> Utilizzare un cluster di macchine virtuali che supportano RDMA in base alle immagini basate su CentOS HPC in Azure Marketplace hello simile toodeploy di passaggi. Come indicato, alcuni passaggi variano leggermente. 
>
>

### <a name="prerequisites"></a>Prerequisiti
* **Computer client**: È necessario un toocommunicate di computer client di Windows, Linux o Mac con Azure. Nella procedura si presuppone che venga usato un client Linux.
* **Sottoscrizione di Azure**: se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti. Per cluster di maggiori dimensioni, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto.
* **Disponibilità di dimensioni VM**: hello seguendo le dimensioni di istanza è in grado di supportare RDMA: H16r, H16mr, A8 e A9. Per informazioni sulla disponibilità nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) .
* **Quota di core**: potrebbe essere necessario quota hello tooincrease di core toodeploy un cluster di macchine virtuali con utilizzo intensivo di calcolo. Ad esempio, è necessario disporre di almeno 128 core se si desidera che le macchine virtuali A9 toodeploy 8 come illustrato in questo articolo. La sottoscrizione anche potrebbe limitare il numero di hello di core, che è possibile distribuire in determinati gruppi di dimensioni macchina virtuale incluso hello H serie. aumentare la quota toorequest, [aprire una richiesta di supporto clienti online](../../../azure-supportability/how-to-create-azure-support-request.md) senza alcun costo.
* **CLI di Azure**: [installare](../../../cli-install-nodejs.md) hello Azure CLI e [tooyour sottoscrizione di Azure connettersi](../../../xplat-cli-connect.md) da computer client hello.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Provisioning di una macchina virtuale HPC SLES 12 SP1
Dopo aver effettuato l'accesso tooAzure con hello CLI di Azure, eseguire `azure config list` tooconfirm che hello l'output mostra la modalità di gestione del servizio. In caso contrario, impostare la modalità hello eseguendo questo comando:

    azure config mode asm


Digitare hello seguente toolist tutte le sottoscrizioni di hello si è autorizzati toouse:

    azure account list

sottoscrizione attiva corrente Hello viene identificato con `Current` impostare troppo`true`. Se la sottoscrizione non hello quello che si desidera toouse toocreate hello cluster, impostare l'ID di sottoscrizione appropriata hello come sottoscrizione attiva hello:

    azure account set <subscription-Id>

toosee hello disponibile pubblicamente immagini SLES 12 SP1 HPC in Azure, eseguire un comando simile hello segue, presupponendo che l'ambiente della shell offre il supporto **grep**:

    azure vm image list | grep "suse.*hpc"

Eseguire il provisioning di una macchina virtuale che supportano RDMA con un'immagine SLES 12 SP1 HPC eseguendo un comando simile hello seguente:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Dove:

* Hello dimensioni (in questo esempio, A9) è una delle dimensioni delle macchine Virtuali che supportano RDMA hello.
* numero di porta esterna SSH Hello (22 in questo esempio è hello SSH predefinito) è qualsiasi numero di porta valido. numero di porta SSH interno Hello è impostato too22.
* Un nuovo servizio cloud viene creato in hello specificato dal percorso hello regione di Azure. Specificare un percorso in cui hello VM dimensione che scelto è disponibile.
* Per il supporto per le priorità SUSE (che comporta costi aggiuntivi), nome dell'immagine hello SLES 12 SP1 attualmente può essere una di queste due opzioni: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Personalizzare hello VM
Al termine hello VM provisioning, SSH toohello VM utilizzando hello l'indirizzo IP esterno della macchina virtuale (o nome DNS) e hello numero di porta esterna configurato e quindi personalizzarlo. Per informazioni di connessione, vedere [come toolog nella macchina virtuale tooa che eseguono Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Eseguire i comandi come utente hello che è configurato su hello macchina virtuale, a meno che l'accesso alla directory radice è necessario toocomplete un passaggio.

> [!IMPORTANT]
> Microsoft Azure non fornisce accesso alla directory radice tooLinux VM. toogain accesso amministrativo quando si è connessi come un toohello utente macchina virtuale, eseguita i comandi tramite `sudo`.
>
>

* **Aggiornamenti**: installare gli aggiornamenti usando zypper. È inoltre possibile utilità NFS tooinstall.

  > [!IMPORTANT]
  > In una VM di HPC SLES 12 SP1, è consigliabile non applicare gli aggiornamenti del kernel, che possono causare problemi con hello Linux RDMA driver.
  >
  >
* **Intel MPI**: completare l'installazione di hello di Intel MPI su hello SLES 12 SP1 HPC VM eseguendo hello comando seguente:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Bloccare la memoria**: per MPI codici toolock hello memoria disponibile per RDMA, aggiungere o modificare hello seguendo le impostazioni nel file /etc/security/limits.conf hello. È necessario tooedit accesso principale di questo file.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > A scopo di test, è anche possibile impostare memlock toounlimited. Ad esempio: `<User or group name>    hard    memlock unlimited`. Per altre informazioni, vedere [Metodi noti per l'impostazione delle dimensioni della memoria bloccata](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **Le chiavi SSH per le macchine virtuali SLES**: generare SSH chiavi tooestablish attendibilità per l'account utente di hello nodi di calcolo nel cluster SLES hello durante l'esecuzione di processi MPI. Se è stata distribuita una macchina virtuale HPC basata su CentOS, non seguire questo passaggio. Dopo aver acquisito immagine hello e distribuire hello cluster, vedere le istruzioni più avanti in questo articolo di tooset di passwordless SSH trust tra i nodi del cluster hello.

    chiavi SSH toocreate, eseguire hello comando seguente. Quando viene richiesto per l'input, selezionare **invio** chiavi hello toogenerate nel percorso predefinito di hello senza impostare una password.

        ssh-keygen

    Accodare il file authorized_keys toohello chiave pubblica di hello per le chiavi pubbliche note.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    Nella directory ~/.ssh hello, modificare o creare file di configurazione hello. Fornire intervallo di indirizzi IP hello della rete privata hello pianificare toouse in Azure (10.32.0.0/16 in questo esempio):

        host 10.32.0.*
        StrictHostKeyChecking no

    In alternativa, elenco indirizzo IP di rete privata hello di ogni macchina virtuale del cluster come indicato di seguito:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > La configurazione di `StrictHostKeyChecking no` può creare un potenziale rischio di sicurezza quando non viene specificato un intervallo o un indirizzo IP specifico.
  >
  >
* **Applicazioni**: installare le applicazioni, è necessario o eseguire altre personalizzazioni prima di acquisire l'immagine di hello.

### <a name="capture-hello-image"></a>Acquisire l'immagine di hello
immagine di hello toocapture, eseguire innanzitutto hello comando seguente in hello VM Linux. Questo comando annullamento del provisioning hello VM ma mantiene gli account utente e le chiavi SSH impostati.

```
sudo waagent -deprovision
```

Dal computer client eseguire hello seguente immagine di hello toocapture comandi CLI di Azure. Per ulteriori informazioni, vedere [come una macchina virtuale di Linux classica come immagine toocapture](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Dopo aver eseguito questi comandi, immagine di macchina virtuale hello viene acquisito per l'uso e hello VM viene eliminato. Ora è disponibile il toodeploy pronto immagine personalizzata un cluster.

### <a name="deploy-a-cluster-with-hello-image"></a>Distribuire un cluster con immagine di hello
Modificare lo script Bash con valori appropriati per l'ambiente seguente hello ed eseguirlo dal computer client. Poiché Azure consente di distribuire macchine virtuali di hello in sequenza nel modello di distribuzione classica hello, sono necessari alcuni minuti toodeploy hello otto macchine virtuali A9 suggerite in questo script.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Considerazioni per un cluster HPC CentOS
Se si vuole tooset di un cluster basato su una delle immagini basate su CentOS HPC hello in hello Azure Marketplace anziché SLES 12 per HPC, seguire i passaggi generali hello hello precedente sezione. Si noti hello seguenti differenze. effettuare il provisioning e configurare hello VM:

- Intel MPI è già installato in una macchina virtuale con provisioning da un'immagine HPC basata su CentOS.
- Le impostazioni della memoria di blocco già aggiunti nel file /etc/security/limits.conf hello della macchina virtuale.
- Non generare le chiavi SSH in hello VM viene effettuato il provisioning per l'acquisizione. È invece consigliabile configurare l'autenticazione basata su utente dopo la distribuzione di cluster hello. Per ulteriori informazioni, vedere hello seguente sezione.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Configurare passwordless trust SSH nel cluster hello
In un cluster HPC basato su CentOS, sono disponibili due metodi per stabilire il trust tra i nodi di calcolo hello: l'autenticazione basata su host e l'autenticazione basata sull'utente. L'autenticazione basata su host esula dall'ambito di hello di questo articolo e in genere deve essere eseguita tramite uno script di estensione durante la distribuzione. L'autenticazione basata su utente è utile per stabilire il trust dopo la distribuzione e richiede la generazione di hello e la condivisione di chiavi SSH tra hello nodi di calcolo nel cluster hello. Questo metodo è comunemente noto come accesso SSH senza password ed è obbligatorio quando si eseguono processi MPI.

È disponibile in uno script di esempio fornito dalla community di hello [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable l'autenticazione utente semplice in un cluster basato su CentOS HPC. Scaricare e usare questo script usando hello alla procedura seguente. È inoltre possibile modificare lo script o usare qualsiasi altro metodo tooestablish passwordless autenticazione SSH tra i nodi di calcolo cluster hello.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

script di hello toorun, è necessario prefisso hello tooknow per gli indirizzi IP di subnet. Ottenere il prefisso hello eseguendo hello comando seguente in uno dei nodi del cluster hello. L'output dovrebbe essere simile al seguente 10.1.3.5 e prefisso hello è parte di hello 10.1.3.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

A questo punto eseguire script hello utilizzando tre parametri: hello comuni nel nome utente hello nodi di calcolo, di password comuni hello per nodi di calcolo di tale utente per hello e prefisso di subnet di hello che è stata restituita dal comando precedente hello.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Questo script hello seguenti:

* Crea una directory nel nodo host hello denominato .ssh, che è necessario per l'account di accesso passwordless.
* Crea un file di configurazione nella directory .ssh hello che indica l'account di accesso tooallow passwordless account di accesso da qualsiasi nodo nel cluster hello.
* Crea i file contenenti i nomi dei nodi di hello e gli indirizzi IP di nodo per tutti i nodi nel cluster hello hello. Questi file vengono lasciati dopo l'esecuzione di script hello per riferimento futuro.
* Crea una coppia di chiavi pubblica e privata per ogni nodo del cluster (inclusi nodo host hello) e crea voci nel file authorized_keys hello.

> [!WARNING]
> L'esecuzione di questo script può creare un potenziale rischio per la sicurezza. Verificare che informazioni sulle chiavi pubbliche hello in ~/.ssh non viene distribuite.
>
>

## <a name="configure-intel-mpi"></a>Configurare Intel MPI
toorun di applicazioni MPI in Azure Linux RDMA, è necessario tooconfigure determinati tooIntel specifico MPI variabili di ambiente. Ecco un toorun hello variabili necessite tooconfigure script di esempio Bash un'applicazione. Modificare toompivars.sh percorso hello in base alle esigenze per l'installazione di Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

formato di Hello del file host hello è come indicato di seguito. Aggiungere una riga per ciascun nodo del cluster. Specificare gli indirizzi IP privati da rete virtuale hello definita in precedenza, non i nomi DNS. Ad esempio, per due host con gli indirizzi IP 10.32.0.1 e 10.32.0.2, file hello contiene seguente hello:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Eseguire MPI su un cluster di base a due nodi
Se non già stato fatto, innanzitutto impostare hello ambiente per Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Eseguire un comando MPI
Eseguire un comando MPI in uno dei tooshow di nodi di calcolo hello MPI sia installato correttamente e possono comunicare tra almeno due nodi di calcolo. esempio Hello **mpirun** comando esegue hello **hostname** comando due nodi.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
L'output deve includere nomi di hello di tutti i nodi di hello che è stato passato come input per `-hosts`. Ad esempio, un **mpirun** comando con due nodi restituisce un output simile hello seguente:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Eseguire un benchmark MPI
Hello Intel MPI comando seguente esegue una pingpong benchmark tooverify hello configurazione e connessione toohello RDMA rete cluster.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

In un cluster di lavoro con due nodi, si dovrebbe vedere l'output seguente hello. In hello rete RDMA di Azure, prevede latenza inferiore o uguale a 3 microsecondi per le dimensioni dei messaggi too512 byte.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Passaggi successivi
* Distribuire ed eseguire le applicazioni MPI Linux nel cluster Linux.
* Vedere hello [documentazione libreria MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) per informazioni aggiuntive sul Intel MPI.
* Provare un [modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un lucentezza Intel cluster mediante un'immagine basata su CentOS HPC. Per informazioni dettagliate, vedere [Distribuzione di Intel Cloud Edition per Lustre in Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).
