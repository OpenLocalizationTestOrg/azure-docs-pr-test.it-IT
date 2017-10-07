---
title: aaaUse SSH con Hadoop - HDInsight di Azure | Documenti Microsoft
description: "È possibile accedere a HDInsight tramite Secure Shell (SSH). Questo documento fornisce informazioni sulla connessione tooHDInsight utilizzando hello ssh e i comandi scp dai client di Windows, Linux, Unix o macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: comandi Hadoop in Linux, comandi Linux per Hadoop, Hadoop in macOS, Hadoop SSH, cluster Hadoop SSH
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Connettersi tooHDInsight (Hadoop) tramite SSH

Informazioni su come toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely connettersi tooHadoop in Azure HDInsight. 

HDInsight è possibile utilizzare (Ubuntu) Linux come sistema operativo hello nodi all'interno di un cluster Hadoop hello. Hello nella tabella seguente contiene informazioni di indirizzo e la porta di hello necessarie durante la connessione basata su tooLinux HDInsight utilizzando un client SSH:

| Indirizzo | Porta | Connessione a |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Nodo perimetrale (R Server in HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Nodo perimetrale (qualsiasi tipo di cluster, se è presente un nodo perimetrale) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Nodo head primario |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Nodo head secondario |

> [!NOTE]
> Sostituire `<edgenodename>` con nome hello del nodo di hello del bordo.
>
> Sostituire `<clustername>` con nome hello del cluster.
>
> Se il cluster contiene un nodo del bordo, è consigliabile che si __si connettono sempre nodo edge toohello__ tramite SSH. i nodi head Hello ospitano servizi di integrità critico toohello di Hadoop. nodo del bordo Hello viene eseguito solo gli elementi da inserire su di esso.
>
> Per altre informazioni sull'uso dei nodi perimetrali, vedere l'articolo su come [usare nodi perimetrali in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>Client SSH

I sistemi Linux, Unix e macOS forniscono hello `ssh` e `scp` comandi. Hello `ssh` client è comunemente utilizzati toocreate una sessione della riga di comando remota con un Linux o Unix-based system. Hello `scp` client è toosecurely utilizzato la copia di file tra client e hello sistema remoto.

Per impostazione predefinita, Microsoft Windows non offre client SSH. Hello `ssh` e `scp` i client sono disponibili per Windows tramite hello pacchetti seguenti:

* [Azure Cloud Shell](../cloud-shell/quickstart.md): hello Shell Cloud fornisce un ambiente Bash nel browser e hello `ssh`, `scp`e altri comandi di Linux.

* [Barra rovesciata in Ubuntu in Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` e `scp` comandi sono disponibili tramite hello Bash nella riga di comando di Windows.

* [GIT (https://git-scm.com/)](https://git-scm.com/): hello `ssh` e `scp` comandi sono disponibili tramite riga di comando GitBash hello.

* [GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` e `scp` comandi sono disponibili tramite riga di comando di Shell di GitHub hello. GitHub Desktop può essere configurato toouse Bash, hello prompt dei comandi di Windows o di PowerShell come riga di comando hello hello Git Shell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell team consiste nel porting OpenSSH tooWindows e fornisce versioni di test.

    > [!WARNING]
    > pacchetto OpenSSH Hello include componente server SSH hello `sshd`. Questo componente viene avviato un server SSH sul sistema, consentire ad altri tooconnect tooit. Non configurare il componente o aprire la porta 22 a meno che non si desidera toohost un server SSH sul sistema. Non è necessario toocommunicate con HDInsight.

Sono disponibili anche diversi client SSH con interfaccia grafica, come [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) e [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Sebbene questi client possono essere utilizzati tooconnect tooHDInsight, processo hello di connessione è diversa rispetto all'utilizzo di hello `ssh` utilità. Per ulteriori informazioni, vedere la documentazione di hello del client con interfaccia grafica di hello in uso.

## <a id="sshkey"></a>Autenticazione: chiavi SSH

Usano SSH chiavi [crittografia a chiave pubblica](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessioni. Le chiavi SSH sono più sicure rispetto alle password e forniscono un modo semplice toosecure accesso tooyour un cluster Hadoop.

Se l'account SSH è protetto tramite una chiave, il client di hello deve fornire hello corrispondente chiave privata, quando ci si connette:

* La maggior parte dei client può essere configurato toouse un __chiave predefinita__. Ad esempio, hello `ssh` client esegue la ricerca di una chiave privata in `~/.ssh/id_rsa` in ambienti Linux e Unix.

* È possibile specificare hello __chiave privata di percorso tooa__. Con hello `ssh` client, hello `-i` parametro è utilizzato toospecify hello percorso tooprivate chiave. ad esempio `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Se si hanno __più chiavi private__ per server diversi, considerare la possibilità di usare un'utilità come [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Hello `ssh-agent` utilità può essere utilizzato tooautomatically hello selezionare chiave toouse quando viene stabilita una sessione SSH.

> [!IMPORTANT]
>
> Se si protegge la chiave privata con una passphrase, è necessario immettere la passphrase hello quando si utilizza chiave hello. Utilità, ad esempio `ssh-agent` può memorizzare nella cache password hello per comodità.

### <a name="create-an-ssh-key-pair"></a>Creare una coppia di chiavi SSH

Hello utilizzare `ssh-keygen` comando toocreate file chiave pubblica e privata. Hello comando che segue genera una coppia di chiavi RSA a 2048 bit che può essere utilizzata con HDInsight:

    ssh-keygen -t rsa -b 2048

Richiesto per le informazioni durante il processo di creazione della chiave hello. Ad esempio, in cui sono archiviate chiavi hello o se toouse una passphrase. Al termine del processo di hello, vengono creati due file. una chiave pubblica e una chiave privata.

* Hello __chiave pubblica__ è toocreate usato un cluster HDInsight. la chiave pubblica di Hello ha un'estensione `.pub`.

* Hello __chiave privata__ è usato tooauthenticate cluster HDInsight toohello client.

> [!IMPORTANT]
> È possibile proteggere le chiavi con una passphrase, che è di fatto una password per la chiave privata. Anche se un utente ha ottenuto la chiave privata, devono avere una chiave di hello passphrase toouse hello.

### <a name="create-hdinsight-using-hello-public-key"></a>Creare utilizzando la chiave pubblica di hello HDInsight

| Metodo di creazione | Come toouse hello chiave pubblica |
| ------- | ------- |
| **Portale di Azure** | Deselezionare __usare stessa password account di accesso cluster__, quindi selezionare __chiave pubblica__ come tipo di autenticazione SSH hello. Infine, selezionare il file di chiave pubblica di hello o incollare il contenuto di testo hello del file hello in hello __chiave pubblica SSH__ campo.</br>![Finestra di dialogo per la chiave pubblica SSH nella creazione di cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Hello utilizzare `-SshPublicKey` parametro di hello `New-AzureRmHdinsightCluster` cmdlet e passare contenuto hello di chiave pubblica di hello sotto forma di stringa.|
| **Interfaccia della riga di comando di Azure 1.0** | Hello utilizzare `--sshPublicKey` parametro di hello `azure hdinsight cluster create` comandi e passare il contenuto di hello di chiave pubblica hello sotto forma di stringa. |
| **Modello di Resource Manager** | Per un esempio dell'uso di SSH con un modello, vedere l'articolo su come [distribuire HDInsight in Linux con una chiave SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/). Hello `publicKeys` elemento hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file è utilizzato toopass hello chiavi tooAzure durante la creazione di cluster hello. |

## <a id="sshpassword"></a>Autenticazione: password

Gli account SSH possono essere protetti con una password. Quando ci si connette tramite SSH tooHDInsight, si è password hello tooenter richiesta.

> [!WARNING]
> Non è consigliabile usare l'autenticazione tramite password per SSH. Le password possono essere individuate e attacchi di forza toobrute vulnerabile. È consigliabile usare invece [chiavi SSH per l'autenticazione](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Creare cluster HDInsight con una password

| Metodo di creazione | Come toospecify hello password |
| --------------- | ---------------- |
| **Portale di Azure** | Per impostazione predefinita, hello account utente SSH è hello stessa password dell'account di accesso cluster hello. toouse una password diversa, deselezionare __usare stessa password account di accesso cluster__, quindi immettere la password di hello in hello __password SSH__ campo.</br>![Finestra di dialogo per la password SSH nella creazione di cluster HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Hello utilizzare `--SshCredential` parametro di hello `New-AzureRmHdinsightCluster` cmdlet e passare un `PSCredential` oggetto che contiene nome dell'account utente SSH hello e una password. |
| **Interfaccia della riga di comando di Azure 1.0** | Hello utilizzare `--sshPassword` parametro di hello `azure hdinsight cluster create` comando e specificare il valore di password hello. |
| **Modello di Resource Manager** | Per un esempio dell'uso di una password con un modello, vedere l'articolo su come [distribuire HDInsight in Linux con una password SSH](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). Hello `linuxOperatingSystemProfile` elemento hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file è utilizzato toopass hello SSH account nome e la password tooAzure durante la creazione di cluster hello.|

### <a name="change-hello-ssh-password"></a>Modificare la password SSH hello

Per informazioni sulla modifica delle password dell'account utente SSH hello, vedere hello __modificare le password__ sezione di hello [gestire HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) documento.

## <a id="domainjoined"></a>Autenticazione: HDInsight aggiunto al dominio

Se si utilizza un __dominio cluster HDInsight__, è necessario utilizzare hello `kinit` comando dopo la connessione con SSH. Questo comando viene richiesto per un utente di dominio e una password e la sessione di autenticazione con il dominio di Azure Active Directory hello associato hello cluster.

Per altre informazioni, vedere [Configurare i cluster HDInsight aggiunti al dominio](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Connettersi toonodes

Hello nodi head e nodo del bordo (se presente) è possibile accedere tramite hello internet sulle porte 22 e 23.

* Quando ci si connette toohello __nodi head__, utilizzare la porta __22__ toohello tooconnect primario head nodo e la porta __23__ nodo head di tooconnect toohello secondario. è Hello toouse nome di dominio completo `clustername-ssh.azurehdinsight.net`, dove `clustername` hello nome del cluster.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Quando connectiung toohello __nodo bordo__, utilizzare la porta 22. è Hello nome di dominio completo `edgenodename.clustername-ssh.azurehdinsight.net`, dove `edgenodename` è un nome specificato quando la creazione di nodo di hello del bordo. `clustername`è il nome di hello del cluster di hello.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Negli esempi precedenti di Hello si presuppone che si utilizza l'autenticazione di password o che l'autenticazione del certificato è che si verificano automaticamente. Se si utilizza una coppia di chiavi SSH per l'autenticazione e certificato di hello non viene utilizzato automaticamente, utilizzare hello `-i` chiave privata del parametro toospecify hello. ad esempio `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Una volta connessi, hello prompt cambia, tooindicate hello SSH utente nome hello nodo e che si è connessi. Ad esempio, quando si è connessi toohello primario nodo head come `sshuser`, prompt dei comandi hello è `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Connettere tooworker e nodi Zookeeper

Hello nodi di lavoro e i nodi non sono direttamente accessibili da Zookeeper hello internet. È possibile accedervi da nodi head del cluster di hello o bordo. di seguito Hello sono nodi tooother tooconnect di hello passaggi generali:

1. Usare SSH tooconnect tooa head o edge nodo:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Da hello head toohello di connessione SSH o nodo edge, usare hello `ssh` comando tooconnect tooa lavoro nodo hello cluster:

        ssh sshuser@wn0-myhdi

    un elenco di nomi di dominio hello di hello nodi cluster hello, tooretrieve vedere hello [hello di gestire HDInsight con Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) documento.

Se l'account SSH hello è protetta tramite un __password__, immettere la password di hello quando ci si connette.

Se hello account SSH è protetto tramite __chiavi SSH__, assicurarsi che l'inoltro SSH è abilitata nel client hello.

> [!NOTE]
> Un altro modo toodirectly accedere a tutti i nodi cluster hello è tooinstall HDInsight in una rete virtuale di Azure. Quindi, è possibile unire toohello il computer remoto stesso virtuale di rete e accedere direttamente a tutti i nodi cluster hello.
>
> Per altre informazioni, vedere l'articolo su come [usare una rete virtuale con HDInsight](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>Configurare l'inoltro dell'agente SSH

> [!IMPORTANT]
> Hello passaggi seguenti si presuppongono un Linux o UNIX-based system e lavorare con Bash in Windows 10. Se questi passaggi non funzionano per il sistema, potrebbe essere documentazione hello tooconsult per il client SSH.

1. Usando un editor di testo, aprire `~/.ssh/config`. Se questo file non esiste, è possibile crearlo immettendo `touch ~/.ssh/config` nella riga di comando.

2. Aggiungere i seguenti toohello testo hello `config` file.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Sostituire hello __Host__ informazioni con indirizzo hello del nodo hello ci si connette toousing SSH. esempio precedente Hello utilizza nodo edge hello. Questa voce consente di configurare l'agente di inoltro per il nodo specificato hello SSH.

3. Test dell'agente SSH inoltro tramite hello comando seguente da hello terminal:

        echo "$SSH_AUTH_SOCK"

    Questo comando restituisce toohello di informazioni simili seguente testo:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Se non viene restituita alcuna informazione, `ssh-agent` non è in esecuzione. Per ulteriori informazioni, vedere informazioni script di avvio agente hello in [utilizzando ssh-agent con ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) o consultare la documentazione di client SSH.

4. Dopo avere verificato che **ssh agente** è in esecuzione, utilizzare hello seguente tooadd l'agente toohello chiave privata SSH:

        ssh-add ~/.ssh/id_rsa

    Se la chiave privata è archiviata in un file diverso, sostituire `~/.ssh/id_rsa` con file di toohello hello del percorso.

5. Connettersi toohello cluster edge o nodi head con SSH. Utilizzare quindi il lavoro tooa tooconnect di hello SSH comando o nodo zookeeper. connessione di Hello viene stabilita tramite chiave hello inoltrato.

## <a name="copy-files"></a>Copiare i file

Hello `scp` utilità può essere utilizzato toocopy file tooand dai singoli nodi di cluster hello. Ad esempio, hello successivo comando copie hello `test.txt` directory dal nodo head primario toohello hello sistema locale:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Poiché è specificato alcun percorso dopo hello `:`, file hello viene inserito nella hello `sshuser` home directory.

Hello seguenti esempio copie hello `test.txt` file hello `sshuser` home directory nel sistema locale di hello nodo head primario toohello:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`può accedere solo hello file system dei singoli nodi all'interno di cluster hello. Non può essere tooaccess utilizzati dati nel servizio di archiviazione per cluster hello hello HDFS compatibile.
>
> Utilizzare `scp` quando è necessario tooupload una risorsa per l'utilizzo in una sessione SSH. Ad esempio, caricare uno script Python e quindi eseguire script hello da una sessione SSH.
>
> Per informazioni sul caricamento dei dati direttamente in hello archiviazione HDFS compatibili, vedere hello seguenti documenti:
>
> * [HDInsight con Archiviazione di Azure](hdinsight-hadoop-use-blob-storage.md).
>
> * [HDInsight con Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Passaggi successivi

* [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)
* [Usare una rete virtuale con HDInsight](hdinsight-extend-hadoop-virtual-network.md)
* [Usare nodi perimetrali in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node)