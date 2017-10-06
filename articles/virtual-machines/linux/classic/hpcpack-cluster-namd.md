---
title: aaaNAMD con Microsoft HPC Pack nelle macchine virtuali Linux | Documenti Microsoft
description: "Informazioni su come distribuire un cluster Microsoft HPC Pack in Azure e come eseguire una simulazione NAMD con charmrun in più nodi di calcolo Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure
Questo articolo illustra un modo toorun un carico di lavoro (HPC) high-performance computing Linux su macchine virtuali di Azure. In questo caso, impostare un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure con nodi di calcolo Linux ed eseguire un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate simulazione e visualizzare hello struttura di un sistema biomolecular di grandi dimensioni.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (per il programma di Dynamics molecolare Nanoscale) è un pacchetto parallelo dynamics molecolare progettato per la simulazione dei sistemi di grandi dimensioni biomolecular ad alte prestazioni che contengono backup toomillions atomi di. Esempi di questi sistemi includono virus, strutture di celle e proteine di grandi dimensioni. NAMD scala toohundreds di core per tipico simulazioni e toomore di 500.000 core per simulazioni di hello più grande.
* **Microsoft HPC Pack** fornisce funzionalità toorun HPC su larga scala e le applicazioni parallele in cluster di computer locali o di macchine virtuali di Azure. Sviluppato originariamente come soluzione per i carichi di lavoro HPC di Windows, HPC Pack supporta ora le applicazioni HPC che eseguono Linux su macchine virtuali del nodo di calcolo Linux distribuite in un cluster HPC Pack. Per una panoramica, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md) .

Per altre toorun opzioni HPC Linux carichi di lavoro in Azure, vedere [risorse tecniche per batch e high performance computing](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Prerequisiti
* **Cluster HPC Pack con nodi di calcolo Linux**: distribuire un cluster HPC Pack con nodi di calcolo Linux in Azure usando un [modello di Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o uno [script di Azure PowerShell](hpcpack-cluster-powershell-script.md). Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per hello prerequisiti e i passaggi per entrambe le opzioni. Se si sceglie l'opzione di distribuzione di script di PowerShell hello, vedere file di configurazione di esempio hello nei file di esempio hello alla fine di hello di questo articolo. Questo file consente di configurare un cluster HPC Pack basato su Azure costituito da un nodo head di Windows Server 2012 R2 e quattro nodi di calcolo CentOS 6.6 di grandi dimensioni. Personalizzare questo file in base all'ambiente in uso.
* **File di esercitazione e software NAMD** -software scaricare NAMD per Linux da hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) sito (è richiesta la registrazione). In questo articolo si basa sul NAMD versione 2.10 e utilizza hello [Linux-x86_64 (64 bit Intel o AMD con Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archivio. Inoltre scaricare hello [file delle esercitazioni NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). download Hello sono file con estensione tar, sono necessari un file hello tooextract dello strumento di Windows nel nodo head del cluster hello. file hello tooextract, seguire le istruzioni di hello più avanti in questo articolo. 
* **VMD** (facoltativo): risultati hello toosee del processo NAMD, scaricare e installare il programma di visualizzazione molecolare hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) in un computer di propria scelta. la versione corrente di Hello è 1.9.2. Vedere hello VMD scaricare tooget sito avviata.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configurare il trust reciproco tra i nodi di calcolo
Esecuzione di un processo tra nodi in più nodi di Linux richiede hello nodi tootrust tra loro (da **rsh** o **ssh**). Quando si crea il cluster di HPC Pack hello con script di distribuzione IaaS di Microsoft HPC Pack hello, script hello imposta automaticamente permanente reciproca relazione di trust per l'account amministratore hello specificato. Per gli utenti non amministratori creati nel dominio del cluster di hello, è necessario tooset temporaneo reciproca relazione di trust tra i nodi di hello quando un processo viene allocato toothem. Infine, l'eliminazione di relazione hello al termine il processo di hello. toodo, per ogni utente, fornire un cluster di toohello coppia di chiavi RSA quali HPC Pack usa una relazione di trust tooestablish hello. Di seguito sono riportate le istruzioni.

### <a name="generate-an-rsa-key-pair"></a>Generare una coppia di chiavi RSA
È facile toogenerate una coppia di chiavi RSA, che contiene una chiave pubblica e una chiave privata, eseguendo hello Linux **ssh-keygen** comando.

1. Accedere tooa computer Linux.
2. Eseguire hello comando seguente:
   
   ```bash
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
1. [Connessione Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo head VM utilizzando hello le credenziali di dominio fornito al momento della distribuzione cluster hello (ad esempio, hpc\clusteradmin). Gestire i cluster di hello dal nodo head hello.
2. Usare toocreate procedure di Windows Server standard account utente di dominio nel dominio di Active Directory del cluster hello. Ad esempio, è possibile utilizzare hello utente di Active Directory e lo strumento di computer nel nodo head hello. esempi di Hello in questo articolo presuppongono che crei un utente di dominio denominato hpcuser nel dominio hpclab hello (hpclab\hpcuser).
3. Aggiungere il cluster HPC Pack toohello di hello dominio utente come un utente del cluster. Per le istruzioni, vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).
4. Creare un file denominato C:\cred.xml e copia hello RSA dati della chiave al suo interno. È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Aprire un prompt dei comandi e immettere hello comando hello tooset credenziali dati per conto di hello hpclab\hpcuser seguente. Utilizzare hello **extendeddata** toopass parametro hello Nome file hello C:\cred.xml creato per i dati chiave hello.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Questo comando viene completato correttamente senza output. Dopo aver impostato le credenziali di hello per gli account utente di hello che è necessario toorun processi, archiviare file cred.xml hello in un percorso sicuro o eliminarlo.
6. Se è stato generato hello coppia di chiavi RSA in uno dei nodi di Linux, tenere presente le chiavi di hello toodelete dopo aver terminato di utilizzare tali. HPC Pack non configura il trust reciproco se rileva un file id_rsa o id_rsa.pub esistente.

> [!IMPORTANT]
> Non è consigliabile eseguendo un processo di Linux come amministratore del cluster in un cluster condiviso, poiché viene eseguito un processo inviato da un amministratore account radice hello in nodi di Linux hello. Un processo inviato da un utente non amministratore viene eseguito con un account utente locale di Linux con stesso nome utente di un processo di hello hello. In questo caso, HPC Pack imposta reciproca relazione di trust per questo utente di Linux in tutti i nodi di hello allocati toohello processo. È possibile impostare l'utente di Linux hello manualmente nei nodi di Linux hello prima di eseguire il processo di hello o HPC Pack Crea utente hello automaticamente quando il processo di hello viene inviato. HPC Pack Crea utente hello, HPC Pack eliminata dopo il completamento del processo di hello. tooreduce minaccia alla sicurezza, le chiavi vengono rimosse al termine del processo di hello nei nodi hello hello.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configurare una condivisione di file per i nodi Linux
Ora configurare una condivisione file SMB e montare una cartella condivisa di hello in tutti i nodi tooallow hello Linux nodi tooaccess NAMD file Linux con un percorso comune. Di seguito sono passaggi toomount una cartella condivisa nel nodo head hello. Una condivisione è consigliata per le distribuzioni, ad esempio CentOS 6.6 che attualmente non supportano il servizio di Azure File hello. Se i nodi di Linux supportano una condivisione di File di Azure, vedere [come archiviazione di File di Azure con Linux toouse](../../../storage/files/storage-how-to-use-files-linux.md). Per altre opzioni di condivisione dei file con HPC Pack, vedere [Introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).

1. Creare una cartella nel nodo head hello e condividerlo tooEveryone impostando i privilegi di lettura/scrittura. In questo esempio, \\ \\CentOS66HN\Namd è il nome di hello della cartella di hello, dove CentOS66HN è il nome host hello del nodo head hello.
2. Creare una sottocartella denominata namd2 nella cartella condivisa hello. All'interno di namd2, creare un'altra sottocartella namdsample.
3. Estrarre i file NAMD hello nella cartella hello utilizzando una versione di Windows di **tar** o un'altra utilità di Windows che opera su tar archivi. 
   
   * Estrarre troppo archivio tar di hello NAMD\\\\CentOS66HN\Namd\namd2.
   * Estrarre i file delle esercitazioni hello in \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Aprire una finestra di Windows PowerShell ed eseguire i seguenti comandi toomount hello cartella condivisa in nodi di Linux hello hello.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello primo comando crea una cartella denominata /namd2 in tutti i nodi nel gruppo LinuxNodes hello. comando secondo Hello Monta //CentOS66HN/Namd/namd2 cartella hello condivise nella cartella hello con dir_mode e file_mode too777 di set di bit. Hello *username* e *password* in hello comando deve essere credenziali hello di un utente nel nodo head hello.

> [!NOTE]
> Hello "\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell. "\`,"significa hello"," (carattere virgola) è una parte del comando hello.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Creare un toorun script Bash un processo NAMD
Il processo NAMD richiede un *nodelist* file per **charmrun** toouse nodi all'avvio di processi NAMD svariate hello toodetermine. Utilizzare uno script Bash che genera file nodelist hello e viene eseguito **charmrun** con questo file nodelist. È quindi possibile inviare un processo NAMD in HPC Cluster Manager per chiamare questo script.

Utilizzando un editor di testo di propria scelta, è possibile creare uno script Bash nella cartella /namd2 hello contenente i file di programma NAMD hello e denominarlo hpccharmrun.sh. Per una rapida modello di prova, copiare script hpccharmrun.sh di esempio hello fornito alla fine di hello di questo articolo e andare troppo[invia un processo NAMD](#submit-a-namd-job).

> [!TIP]
> Salvare lo script come file di testo con terminazioni riga Linux (solo LF, non CR LF), In questo modo si garantisce il corretto funzionamento in nodi di Linux hello.
> 
> 

Di seguito sono descritte nel dettaglio le operazioni eseguite dallo script Bash. 

1. Definire alcune variabili.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Ottenere informazioni sul nodo dalle variabili di ambiente hello. $NODESCORES archivia un elenco di parole suddivise da $CCP_NODES_CORES. $COUNT è pari a hello $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   formato di Hello per hello $CCP_NODES_CORES variabile è il seguente:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Questa variabile Elenca numero totale di hello di nodi, i nomi dei nodi e numero di core in ogni nodo allocati toohello processo. Ad esempio, se il processo di hello deve 10 core toorun, valore hello $CCP_NODES_CORES è simile a:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Se non è una variabile di hello $CCP_NODES_CORES, avviare **charmrun** direttamente. È consigliabile seguire questa procedura solo quando si esegue lo script direttamente nei nodi Linux.
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. In alternativa, creare un file nodelist per **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Eseguire **charmrun** con file nodelist hello, ottenere lo stato restituito e rimuovere file nodelist hello alla fine di hello.
   
   ${CCP_NUMCPUS} è impostata dal nodo head di HPC Pack hello un'altra variabile di ambiente. Archivia il numero di hello di core totale allocato toothis processo. Usato da numero hello toospecify di processi per charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Uscita con hello **charmrun** restituiscono lo stato.
   
   ```
   exit ${RTNSTS}
   ```

Di seguito è informazioni hello nel file hello nodelist quale script hello genera l'errore:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

ad esempio:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Inviare un processo NAMD
Si è ora pronto toosubmit un processo NAMD in Gestione Cluster HPC.

1. Connettersi tooyour nodo head del cluster e avviare HPC Cluster Manager.
2. In **la gestione delle risorse**, assicurarsi che i nodi di calcolo di hello Linux hello **Online** stato. Se lo stato è diverso, selezionarli e fare clic su **Portare Online**.
3. In **Job Management** (Gestione processi) fare clic su **New Job** (Nuovo processo).
4. Immettere un nome per il processo, ad esempio *hpccharmrun*.
   
   ![Nuovo processo HPC][namd_job]
5. In hello **i dettagli dei processi** nella pagina **risorse di processo**, selezionare il tipo di hello di risorsa come **nodo** e set hello **minimo** too3. , si esegue il processo di hello in tre nodi di Linux e ogni nodo dispone di quattro core.
   
   ![Risorse del processo][job_resources]
6. Fare clic su **modifica attività** in hello spostamento a sinistra e quindi fare clic su **Aggiungi** tooadd un processo toohello di attività.    
7. In hello **i dettagli delle attività e il reindirizzamento i/o** pagina hello set seguenti valori:
   
   * **Riga di comando** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Hello riga di comando precedente è un comando singolo senza interruzioni di riga. Esegue il wrapping tooappear su più righe in **riga di comando**.
     > 
     > 
   * **Working directory** - /namd2
   * **Minimum** - 3
     
     ![Dettagli dell'attività][task_details]
     
     > [!NOTE]
     > Impostare la directory di lavoro hello qui perché **charmrun** tenta toonavigate toohello stessa directory di lavoro in ogni nodo. Se non è impostata, la directory di lavoro hello HPC Pack inizia comando hello in una cartella denominata in modo casuale creata su uno dei nodi di Linux hello. In questo modo l'errore seguente in hello hello altri nodi: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid questo problema, specificare un percorso di cartella accessibile da tutti i nodi come directory di lavoro hello.
     > 
     > 
8. Fare clic su **OK** e quindi fare clic su **Invia** toorun questo processo.
   
   Per impostazione predefinita, HPC Pack invia il processo di hello come account utente corrente. Una finestra di dialogo è possibile che richieda nome utente di tooenter hello e una password dopo aver fatto clic **Invia**.
   
   ![Credenziali del processo][creds]
   
   In alcune condizioni, HPC Pack memorizza informazioni utente di hello prima di input e non visualizza questa finestra di dialogo. toomake HPC Pack visualizzarlo nuovamente, immettere hello comando al Prompt di comando seguente e quindi inviare il processo di hello.
   
   ```command
   hpccred delcreds
   ```
9. il processo di Hello richiede diversi minuti toofinish.
10. Trovare i log di processi hello in \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log e hello output file \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Facoltativamente, avviare VMD tooview i risultati del processo. passaggi di Hello per la visualizzazione dei file di output di hello NAMD (in questo caso, una molecola proteine ubiquitin in una sfera di acqua) esulano dall'ambito hello di questo articolo. Per informazioni dettagliate, vedere l' [esercitazione relativa a NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) .
    
    ![Risultati del processo][vmd_view]

## <a name="sample-files"></a>File di esempio
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>File di configurazione XML di esempio per la distribuzione di cluster tramite script PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
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

### <a name="sample-hpccharmrunsh-script"></a>Script hpccharmrun.sh di esempio
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
