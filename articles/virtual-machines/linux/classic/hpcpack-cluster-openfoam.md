---
title: aaaRun OpenFOAM con HPC Pack nelle macchine virtuali Linux | Documenti Microsoft
description: "Informazioni su come distribuire un cluster Microsoft HPC Pack in Azure ed eseguire un processo OpenFOAM in più nodi di calcolo Linux su una rete RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Eseguire OpenFoam con Microsoft HPC Pack in un cluster Linux RDMA in Azure
Questo articolo illustra un modo toorun OpenFoam macchine virtuali di Azure. Viene distribuito un cluster Microsoft HPC Pack con nodi di calcolo Linux in Azure e viene eseguito un processo [OpenFoam](http://openfoam.com/) con Intel MPI. È possibile utilizzare macchine virtuali di Azure che supportano RDMA per nodi di calcolo hello, in modo che i nodi di calcolo hello comunicano su hello rete RDMA di Azure. Altre opzioni toorun OpenFoam in Azure includono completamente configurato commerciale immagini disponibili in Marketplace, ad esempio del UberCloud hello [OpenFoam 2.3 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)e mediante l'esecuzione su [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (Open Field Operation and Manipulation) è un pacchetto software di fluidodinamica computazionale (CFD) open source ampiamente usato in ambito ingegneristico e scientifico, in organizzazioni sia di tipo commerciale che accademico. Include strumenti per la generazione di mesh, ad esempio snappyHexMesh, uno strumento di generazione mesh parallelizzato per geometrie CAD complesse, per la pre e la post-elaborazione. Quasi tutti i processi eseguiti in parallelo, consentendo agli utenti tootake appieno hardware del computer a loro disposizione.  

Microsoft HPC Pack fornisce funzionalità toorun HPC su larga scala e applicazioni parallele, incluse le applicazioni MPI, nei cluster di macchine virtuali di Microsoft Azure. HPC Pack supporta anche applicazioni HPC che eseguono Linux su macchine virtuali del nodo di calcolo Linux distribuite in un cluster HPC Pack. Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per un'introduzione toousing Linux nodi di calcolo di HPC Pack.

> [!NOTE]
> Questo articolo illustra come toorun un carico di lavoro Linux MPI con HPC Pack. e presuppone che l'utente abbia familiarità con l'amministrazione del sistema Linux e con l'esecuzione di carichi di lavoro MPI in cluster Linux. Se si utilizzano versioni di MPI e OpenFOAM diversi da quelli illustrati in questo articolo hello, potrebbe essere toomodify alcuni passaggi di installazione e configurazione. 
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* **Cluster HPC Pack con nodi di calcolo con supporto per RDMA**: distribuire un cluster HPC Pack con nodi di calcolo Linux di dimensione A8, A9, H16r o H16rm usando un [modello di Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o uno [script di Azure PowerShell](hpcpack-cluster-powershell-script.md). Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per hello prerequisiti e i passaggi per entrambe le opzioni. Se si sceglie l'opzione di distribuzione di script di PowerShell hello, vedere file di configurazione di esempio hello nei file di esempio hello alla fine di hello di questo articolo. Utilizzare questo cluster di HPC Pack toodeploy un basati su Azure configurazione costituito da un nodo head di dimensioni A8 Windows Server 2012 R2 e 2 dimensioni A8 SUSE Linux Enterprise Server 12 nodi di calcolo. Sostituire i valori dell'esempio con i valori appropriati per la sottoscrizione e i nomi dei servizi. 
  
  **Ulteriori operazioni tooknow**
  
  * Per i prerequisiti della rete RDMA Linux in Azure, vedere [Dimensioni delle VM High Performance Computing (HPC)](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Se si utilizza l'opzione di distribuzione di script di Powershell hello, distribuire tutti i nodi di calcolo di Linux hello all'interno di connessione di rete RDMA di un cloud servizio toouse hello.
  * Dopo aver distribuito i nodi di Linux hello, connessione SSH tooperform qualsiasi attività amministrative aggiuntive. Trovare i dettagli della connessione SSH hello per ogni VM Linux nel portale di Azure hello.  
* **Intel MPI** -toorun OpenFOAM su SLES 12 HPC nodi di calcolo in Azure, è necessario tooinstall hello Intel MPI libreria 5 runtime da hello [Intel.com sito](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 è preinstallato nelle immagini HPC basate su CentOS).  Se necessario, in un passaggio successivo installare Intel MPI nei nodi di calcolo Linux. tooprepare per questo passaggio, dopo aver registrato con Intel, seguire il collegamento di hello in hello conferma tramite posta elettronica toohello correlati pagina web. Quindi, hello Copia collegamento per il download per il file .tgz hello hello appropriata per versione di Intel MPI. Questo articolo si riferisce a Intel MPI versione 5.0.3.048.
* **Service Pack di origine OpenFOAM** -scaricare il software di Service Pack di origine OpenFOAM hello per Linux da hello [sito OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/). In questo articolo viene usato Source Pack versione 2.3.1, disponibile per il download come OpenFOAM 2.3.1.tgz. Seguire le istruzioni di hello più avanti in questo articolo di toounpack e compilare OpenFOAM sui nodi di calcolo di hello Linux.
* **EnSight** (facoltativo): risultati hello toosee della simulazione di OpenFOAM, scaricare e installare hello [EnSight](https://www.ceisoftware.com/download/) programma di analisi e visualizzazione. Informazioni sulla gestione delle licenze e download sono presso EnSight hello.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configurare il trust reciproco tra i nodi di calcolo
Esecuzione di un processo tra nodi in più nodi di Linux richiede hello nodi tootrust tra loro (da **rsh** o **ssh**). Quando si crea il cluster di HPC Pack hello con script di distribuzione IaaS di Microsoft HPC Pack hello, script hello imposta automaticamente permanente reciproca relazione di trust per l'account amministratore hello specificato. Per gli utenti non amministratori creati nel dominio del cluster di hello, è possibile tooset temporaneo reciproca relazione di trust tra i nodi di hello quando un processo viene allocato toothem ed Elimina relazione hello dopo che viene completato il processo di hello. trust tooestablish per ogni utente, fornire un cluster di toohello coppia di chiavi RSA utilizzata per la relazione di trust hello HPC Pack.

### <a name="generate-an-rsa-key-pair"></a>Generare una coppia di chiavi RSA
È facile toogenerate una coppia di chiavi RSA, che contiene una chiave pubblica e una chiave privata, eseguendo hello Linux **ssh-keygen** comando.

1. Accedere tooa computer Linux.
2. Eseguire hello comando seguente:
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Premere **invio** toouse impostazioni predefinite di hello fino a quando non viene completato hello. Non immettere una passphrase. Quando viene richiesta una password, è sufficiente premere **Invio**.
   > 
   > 
   
   ![Generare una coppia di chiavi RSA][keygen]
3. Cambiare directory toohello ~/.ssh directory. la chiave privata di Hello viene archiviata nella chiave pubblica id_rsa e hello id_rsa.pub.
   
   ![Chiavi pubbliche e private][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Aggiungere cluster HPC Pack toohello di hello coppia di chiavi
1. Verificare un nodo head di tooyour connessione Desktop remoto con l'account administrator di HPC Pack (hello amministratore account configurato durante l'esecuzione di script di distribuzione hello).
2. Usare toocreate procedure di Windows Server standard account utente di dominio nel dominio di Active Directory del cluster hello. Ad esempio, è possibile utilizzare hello utente di Active Directory e lo strumento di computer nel nodo head hello. esempi di Hello in questo articolo presuppongono che crei un utente di dominio denominato hpclab\hpcuser.
3. Creare un file denominato C:\cred.xml e copia hello RSA dati della chiave al suo interno. Un file di esempio cred.xml è alla fine di hello di questo articolo.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Aprire un prompt dei comandi e immettere hello comando hello tooset credenziali dati per conto di hello hpclab\hpcuser seguente. Utilizzare hello **extendeddata** toopass parametro hello nome del file C:\cred.xml creato per i dati chiave hello.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Questo comando viene completato correttamente senza output. Dopo aver impostato le credenziali di hello per gli account utente di hello che è necessario toorun processi, archiviare file cred.xml hello in un percorso sicuro o eliminarlo.
5. Se è stato generato hello coppia di chiavi RSA in uno dei nodi di Linux, tenere presente le chiavi di hello toodelete dopo aver terminato di utilizzare tali. Se HPC Pack rileva un file id_rsa o id_rsa.pub esistente, non configura il trust reciproco.

> [!IMPORTANT]
> Non è consigliabile eseguendo un processo di Linux come amministratore del cluster in un cluster condiviso, poiché viene eseguito un processo inviato da un amministratore account radice hello in nodi di Linux hello. Tuttavia, un processo inviato da un utente non amministratore viene eseguito con un account utente locale di Linux con hello stesso nome utente di un processo di hello. In questo caso, HPC Pack imposta reciproca relazione di trust per questo utente Linux tra nodi hello allocati toohello processo. È possibile impostare l'utente di Linux hello manualmente nei nodi di Linux hello prima di eseguire il processo di hello o HPC Pack Crea utente hello automaticamente quando il processo di hello viene inviato. HPC Pack Crea utente hello, HPC Pack eliminata dopo il completamento del processo di hello. minacce per la sicurezza tooreduce, HPC Pack rimuove le chiavi di hello dopo il completamento del processo.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configurare una condivisione di file per i nodi Linux
Ora si consiglia di configurare una condivisione SMB standard in una cartella nel nodo head hello. tooallow hello Linux nodi tooaccess file dell'applicazione con un percorso comune, hello montaggio cartella nei nodi Linux hello condivisa. In alternativa, è possibile usare un'altra opzione di condivisione, ad esempio una condivisione File di Azure, consigliata per molti scenari, oppure una condivisione NFS. Vedere il file hello condivisione di informazioni e procedure dettagliate per [Introduzione a Linux nodi di calcolo in un Cluster HPC Pack in Azure](hpcpack-cluster.md).

1. Creare una cartella nel nodo head hello e condividerlo tooEveryone impostando i privilegi di lettura/scrittura. Ad esempio condividere C:\OpenFOAM nel nodo head di hello come \\ \\SUSE12RDMA HN\OpenFOAM. In questo caso, *SUSE12RDMA HN* è il nome host hello del nodo head hello.
2. Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Hello primo comando crea una cartella denominata /openfoam in tutti i nodi nel gruppo LinuxNodes hello. comando secondo Hello Monta //SUSE12RDMA-HN/OpenFOAM cartella hello condiviso in nodi di Linux hello con dir_mode e file_mode too777 di set di bit. Hello *username* e *password* in hello comando deve essere credenziali hello di un utente nel nodo head hello.

> [!NOTE]
> Hello "\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell. "\`,"significa hello"," (carattere virgola) è una parte del comando hello.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Installare MPI e OpenFOAM
toorun OpenFOAM come un processo MPI su rete RDMA hello, è necessario toocompile OpenFOAM con le librerie di Intel MPI hello. 

In primo luogo, eseguire vari **clusrun** comandi OpenFOAM e librerie di Intel MPI tooinstall (se non è già installato) sui nodi di Linux. Condivisione di un nodo head hello utilizzare configurata in precedenza i file di installazione hello tooshare tra i nodi di Linux hello.

> [!IMPORTANT]
> Questi passaggi di installazione e compilazione sono riportati come esempio È necessario una discreta conoscenza di Linux tooensure di amministrazione di sistema che dipendenti compilatori e librerie siano installate correttamente. Potrebbe essere necessario toomodify alcune variabili di ambiente o altre impostazioni per le versioni di Intel MPI e OpenFOAM. Per informazioni dettagliate, vedere [Guida all'installazione di Intel MPI Library per Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) e [Installazione del pacchetto di origine di OpenFOAM](http://openfoam.org/download/2-3-1-source/) per l'ambiente in uso.
> 
> 

### <a name="install-intel-mpi"></a>Installare Intel MPI
Salvare il pacchetto di installazione scaricato hello per Intel MPI (l_mpi_p_5.0.3.048.tgz in questo esempio) in C:\OpenFoam nel nodo head hello in modo che i nodi di Linux hello possono accedere a questo file da /openfoam. Eseguire quindi **clusrun** libreria Intel MPI tooinstall in tutti i nodi di Linux hello.

1. di seguito Hello comandi pacchetto di installazione copia hello e decomprimerlo troppo/rifiutare/intel in ogni nodo.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. Libreria MPI Intel tooinstall invisibile all'utente, utilizzare un file di silent.cfg. È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo. Inserire questo file in hello condivisa /openfoam cartella. Per informazioni dettagliate sul file silent.cfg hello, vedere [Intel MPI libreria per la Guida all'installazione di Linux - installazione invisibile all'utente](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Assicurarsi di salvare il file silent.cfg come file di testo con terminazioni di riga Linux (solo LF, non CR LF), Questo passaggio garantisce che venga eseguito correttamente in nodi di Linux hello.
   > 
   > 
3. Installare Intel MPI Library in modalità invisibile all'utente.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Configurare MPI
Per il test, è consigliabile aggiungere hello seguenti righe toohello /etc/security/limits.conf in ognuno dei nodi di Linux hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Riavviare i nodi di Linux hello dopo l'aggiornamento di file limits.conf hello. Ad esempio, utilizzare la seguente hello **clusrun** comando:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Dopo il riavvio, verificare che tale cartella hello viene montata come /openfoam.

### <a name="compile-and-install-openfoam"></a>Compilare e installare OpenFOAM
Salvare il pacchetto di installazione scaricato hello per hello tooC:\OpenFoam OpenFOAM Source Pack (OpenFOAM 2.3.1.tgz in questo esempio) nel nodo head hello in modo che i nodi di Linux hello possono accedere a questo file da /openfoam. Eseguire quindi **clusrun** comandi hello di toocompile OpenFOAM in tutti i nodi di Linux.

1. Creare una cartella /opt/OpenFOAM in ogni nodo di Linux, Copia cartella toothis hello origine pacchetto ed estrarre i file non esiste.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM con hello libreria MPI Intel, innanzitutto impostare alcune variabili di ambiente per Intel MPI e OpenFOAM. Utilizzare uno script bash denominato settings.sh tooset hello variabili. È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo. Inserire questo file (salvato con terminazioni di riga di Linux) in hello condivisa /openfoam cartella. Questo file contiene inoltre le impostazioni per hello MPI e OpenFOAM runtime utilizzare successive toorun un processo OpenFOAM.
3. Installare pacchetti dipendenti necessiti toocompile OpenFOAM. A seconda di distribuzione di Linux, è necessario innanzitutto tooadd un repository. Eseguire **clusrun** comandi simili toohello seguenti:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Se necessario, hello toorun SSH tooeach Linux nodo comandi tooconfirm cui vengono eseguite correttamente.
4. Comando che segue di esecuzione hello toocompile OpenFOAM. il processo di compilazione Hello accetta alcuni toocomplete ora e genera una grande quantità di informazioni toostandard dell'output di log, pertanto usare hello **/ interleaved** l'opzione di output di hello toodisplay interfogliati.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Hello "\`" simbolo nel comando hello è un simbolo di escape per PowerShell. "\`&" significa hello "e" è una parte del comando hello.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Preparazione di un processo OpenFOAM toorun
Ora get ready toorun un processo MPI chiamato sloshingTank3D, che è uno degli esempi OpenFoam hello, in due nodi di Linux. 

### <a name="set-up-hello-runtime-environment"></a>Configurare un ambiente di runtime hello
tooset ambienti di runtime hello OpenFOAM relative MPI in nodi di Linux hello, Esegui comando in una finestra di Windows PowerShell seguente nel nodo head hello hello. (Questo comando è valido solamente per SUSE Linux).

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Preparare i dati di esempio
Condivisione di un nodo head hello utilizzare configurate in precedenza i file tooshare tra i nodi di Linux hello (montati come /openfoam).

1. Nodi di calcolo SSH tooone del Linux.
2. Se non hai già fatto, eseguire hello tooset di comando di ambiente di runtime OpenFOAM hello, di seguito.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Copiare una cartella condivisa toohello esempio sloshingTank3D hello e passare tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Quando si utilizzano parametri predefiniti hello di questo esempio, può richiedere decine di toorun minuti, pertanto è opportuno toomodify toomake alcuni parametri eseguito più velocemente. Una semplice scelta è toomodify hello ora passaggio variabili deltaT e writeInterval nel file di sistema/controlDict hello. Questo file contiene tutti i dati di input relativi controllo toohello di tempo e di lettura e scrittura di dati della soluzione. Ad esempio, è possibile modificare il valore di hello di deltaT da too0.5 0,05 e il valore di hello di writeInterval da too0.5 0,05.
   
   ![Modificare le variabili delle fasi][step_variables]
5. Specificare i valori desiderati per le variabili di hello nel file di sistema/decomposeParDict hello. In questo esempio vengono utilizzati due nodi di Linux ogni con 8 core, quindi impostare numberOfSubdomains too16 e n di hierarchicalCoeffs too(1 1 16), vale a dire che eseguire OpenFOAM in parallelo con i processi di 16. Per altre informazioni, vedere la sezione [3.4 del manuale dell'utente di OpenFOAM relativa all'esecuzione di applicazioni in parallelo](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).
   
   ![Scomporre i processi][decompose]
6. Eseguire hello dopo i comandi da dati di esempio hello tooprepare directory sloshingTank3D hello.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Nel nodo head hello, dovrebbe essere vengono copiati i file di dati di esempio hello in C:\OpenFoam\sloshingTank3D. (C:\OpenFoam è una cartella condivisa di hello nel nodo head hello.)
   
   ![File di dati sul nodo head hello][data_files]

### <a name="host-file-for-mpirun"></a>File host per mpirun
In questo passaggio è creare un file di host (un elenco di nodi di calcolo) quale hello **mpirun** comando Usa.

1. In uno dei nodi di Linux hello, creare un file denominato file host in /openfoam, pertanto questo file può essere raggiunto al /openfoam/hostfile in tutti i nodi di Linux.
2. Scrivere i nomi dei nodi Linux in questo file. In questo esempio, file hello contiene hello i nomi seguenti:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > È anche possibile creare questo file in C:\OpenFoam\hostfile nel nodo head hello. Se si sceglie questa opzione, è necessario salvare lo script come file di testo con terminazioni di riga Linux (solo LF, non CR LF), In questo modo si garantisce il corretto funzionamento in nodi di Linux hello.
   > 
   > 
   
   **Wrapper di script bash**
   
   Se si dispongano di molti nodi di Linux e si desidera toorun il processo solo per alcune di esse, non è un toouse buona un host predefinito di file, perché non si conoscono i nodi che verranno allocati tooyour processo. In questo caso, scrivere un wrapper di script bash per **mpirun** toocreate hello automaticamente i file di host. È possibile trovare un wrapper di script di esempio bash chiamato hpcimpirun.sh alla fine di hello di questo articolo e salvarlo come /openfoam/hpcimpirun.sh. Questo script di esempio hello seguenti:
   
   1. Consente di impostare le variabili di ambiente hello **mpirun**e un processo MPI hello toorun di addizione comando parametri tramite rete RDMA hello. In questo caso, imposta hello seguenti variabili:
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Crea un file di host in base a toohello $ variabile di ambiente CCP_NODES_CORES, che viene impostato dal nodo head HPC hello quando il processo di hello è attivato.
      
      formato Hello $CCP_NODES_CORES segue questo modello:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      dove
      
      * `<Number of nodes>`-numero di nodi di hello allocata toothis processo.  
      * `<Name of node_n_...>`-nome hello di ogni nodo allocata toothis processo.
      * `<Cores of node_n_...>`-numero di core nel processo di hello nodo toothis allocato hello.
      
      Ad esempio, se il processo di hello necessita di due nodi toorun, $CCP_NODES_CORES è simile a
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Hello chiamate **mpirun** comando e accoda riga di comando di due parametri toohello.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-Crea il percorso di hello di hello host file hello script
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-una variabile di ambiente impostata dal nodo head HPC Pack, hello che archivia il numero di hello di core totale allocato toothis processo. In questo caso, specifica il numero di hello dei processi di **mpirun**.

## <a name="submit-an-openfoam-job"></a>Inviare un processo OpenFOAM
A questo punto è possibile inviare un processo in HPC Cluster Manager. È necessario toopass hello script hpcimpirun.sh nelle righe di comando hello per alcune delle attività di processo hello.

1. Connettersi tooyour nodo head del cluster e avviare HPC Cluster Manager.
2. **Gestione delle risorse**, assicurarsi che i nodi di calcolo di hello Linux hello **Online** stato. Se lo stato è diverso, selezionarli e fare clic su **Portare Online**.
3. In **Job Management** (Gestione processi) fare clic su **New Job** (Nuovo processo).
4. Immettere un nome per il processo, ad esempio *sloshingTank3D*.
   
   ![Dettagli del processo][job_details]
5. In **risorse di processo**, scegliere il tipo di hello di risorsa come "Nodo" e impostare too2 minimo hello. Questa configurazione esegue il processo di hello in due nodi di Linux, ognuno dei quali presenta otto core in questo esempio.
   
   ![Risorse del processo][job_resources]
6. Fare clic su **modifica attività** in hello spostamento a sinistra e quindi fare clic su **Aggiungi** tooadd un processo toohello di attività. Aggiungere quattro processo toohello di attività con hello seguenti righe di comando e le impostazioni.
   
   > [!NOTE]
   > Esecuzione `source /openfoam/settings.sh` imposta hello OpenFOAM e MPI gli ambienti di runtime, in modo ciascuna delle seguenti attività hello chiama prima hello OpenFOAM comando.
   > 
   > 
   
   * **Attività 1**. Eseguire **decomposePar** toogenerate i file di dati per l'esecuzione **interDyMFoam** in parallelo.
     
     * Assegnare un nodo toohello attività
     * **Riga di comando** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Directory di lavoro** - /openfoam/sloshingTank3D
     
     Vedere hello seguente illustrazione. Configurare le attività rimanenti hello in modo analogo.
     
     ![Dettagli dell'attività 1][task_details1]
   * **Attività 2**. Eseguire **interDyMFoam** nell'esempio hello toocompute parallelo.
     
     * Assegnare due nodi toohello attività
     * **Riga di comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Directory di lavoro** - /openfoam/sloshingTank3D
   * **Attività 3**. Eseguire **reconstructPar** toomerge hello imposta delle directory ora da ogni directory processor_N_ in un unico gruppo.
     
     * Assegnare un nodo toohello attività
     * **Riga di comando** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Directory di lavoro** - /openfoam/sloshingTank3D
   * **Attività 4**. Eseguire **foamToEnsight** in parallelo tooconvert file dei risultati OpenFOAM hello in EnSight formattare e hello EnSight file in una directory denominata Ensight nella directory case hello.
     
     * Assegnare due nodi toohello attività
     * **Riga di comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Directory di lavoro** - /openfoam/sloshingTank3D
7. Aggiungere le dipendenze toothese attività in attività ordine crescente.
   
   ![Dipendenze dell'attività][task_dependencies]
8. Fare clic su **Invia** toorun questo processo.
   
   Per impostazione predefinita, HPC Pack invia il processo di hello come account utente corrente. Dopo aver fatto clic **Invia**, si potrebbe visualizzare una finestra di dialogo che richiede nome utente di tooenter hello e una password.
   
   ![Credenziali del processo][creds]
   
   In alcune condizioni, HPC Pack memorizza informazioni utente di hello prima di input e non visualizza questa finestra di dialogo. toomake HPC Pack visualizzarlo nuovamente, immettere hello comando al prompt di comando seguente e quindi inviare il processo di hello.
   
   ```
   hpccred delcreds
   ```
9. processo Hello accetta da decine di minuti tooseveral ore in base a parametri toohello che sono stati impostati per l'esempio hello. Nella mappa di calore hello, vedrai il processo di hello in esecuzione in nodi di Linux hello. 
   
   ![Mappa termica][heat_map]
   
   In ogni nodo vengono avviati otto processi.
   
   ![Processi Linux][linux_processes]
10. Al termine del processo di hello, è possibile trovare i risultati del processo hello nelle cartelle in C:\OpenFoam\sloshingTank3D e file di log hello C:\OpenFoam.

## <a name="view-results-in-ensight"></a>Visualizzare i risultati in EnSight
Se si desidera utilizzare [EnSight](https://www.ceisoftware.com/) toovisualize e analisi dei risultati del processo OpenFOAM hello hello. Per altre informazioni sulla visualizzazione e l'animazione in EnSight, vedere questa [guida video](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Dopo aver installato EnSight nel nodo head hello, avviarlo.
2. Aprire C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Viene visualizzato un serbatoio nel Visualizzatore hello.
   
   ![Serbatoio in EnSight][tank]
3. Creare un **Isosurface** da **internalMesh**, quindi scegliere variabile hello **alpha_water**.
   
   ![Creare un oggetto isosurface][isosurface]
4. Impostare il colore di hello per **Isosurface_part** creato nel passaggio precedente hello. Ad esempio, impostarla toowater blu.
   
   ![Modificare il colore dell'oggetto isosurface][isosurface_color]
5. Creare un **Iso volume** da **pareti** selezionando **pareti** in hello **parti** pannello e fare clic su hello **Isosurfaces**  pulsante nella barra degli strumenti hello.
6. Nella finestra di dialogo hello selezionare **tipo** come **Isovolume** e impostare Min di hello **Isovolume intervallo** too0.5. toocreate hello isovolume, fare clic su **crea con parti selezionate**.
7. Impostare il colore di hello per **Iso_volume_part** creato nel passaggio precedente hello. Ad esempio, impostarla acqua toodeep blu.
8. Impostare il colore di hello per **pareti**. Ad esempio, impostarla tootransparent bianco.
9. Fare clic su **riprodurre** risultati hello toosee di simulazione hello.
   
    ![Risultato per il serbatoio][tank_result]

## <a name="sample-files"></a>File di esempio
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>File di configurazione XML di esempio per la distribuzione di cluster tramite script PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>File cred.xml di esempio
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Esempio silent.cfg file tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Script settings.sh di esempio
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Script hpccharmrun.sh di esempio
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
