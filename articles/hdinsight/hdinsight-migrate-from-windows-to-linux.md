---
title: aaaMigrate da HDInsight basati su Windows basato su tooLinux HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toomigrate da un HDInsight basati su Windows cluster del cluster HDInsight basati su Linux tooa.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Eseguire la migrazione da un cluster basato su Linux di HDInsight basati su Windows cluster tooa

Questo documento vengono fornite informazioni dettagliate sulle differenze tra HDInsight in Windows e Linux e informazioni aggiuntive su come la hello toomigrate i carichi di lavoro tooa basati su Linux cluster esistente.

HDInsight basati su Windows offre un toouse facilmente nel cloud hello Hadoop, potrebbe essere necessario toomigrate tooa basati su Linux cluster. Ad esempio, tootake sfruttare gli strumenti basati su Linux e tecnologie necessarie per la soluzione. Molte operazioni nell'ecosistema Hadoop hello vengono sviluppate nei sistemi basati su Linux e potrebbero non essere disponibile per l'utilizzo con HDInsight basati su Windows. Inoltre, molti libri, video e altre forme di materiale didattico prevedono che si usi un sistema Linux quando si lavora con Hadoop.

> [!NOTE]
> Cluster HDInsight utilizzano supporto a lungo termine Ubuntu (LTS) come sistema operativo hello per nodi hello hello cluster. Per informazioni sulla versione di hello di Ubuntu disponibili con HDInsight, insieme ad altre informazioni di controllo delle versioni del componente, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Attività di migrazione

flusso di lavoro generale Hello per la migrazione è come indicato di seguito.

![Diagramma del flusso di lavoro della migrazione](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Leggere ogni sezione di questo documento toounderstand modifiche che possono essere necessari durante la migrazione del flusso di lavoro esistente, i processi, cluster basati su Linux tooa di e così via.

2. Creare un cluster basato su Linux come ambiente di test/controllo qualità. Per altre informazioni sulla creazione di un cluster basato su Linux, vedere [Creare cluster Hadoop basati su Linux in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Copia esistente processi, origini dati e sink toohello nuovo ambiente.

4. Eseguire test toomake assicurarsi che i processi di funzionano come previsto nel nuovo cluster hello di convalida.

Dopo avere verificato che tutto funzioni come previsto, pianificare i tempi di inattività per la migrazione di hello. Durante questo periodo di inattività, eseguire hello seguenti azioni:

1. Eseguire il backup dei dati temporanei archiviati in locale sui nodi del cluster hello. ad esempio se i dati sono archiviati direttamente in un nodo head.

2. Eliminare il cluster basati su Windows hello.

3. Creare un cluster basato su Linux utilizzando hello stessa impostazione predefinita l'archivio dati che hello cluster basati su Windows utilizzato. cluster basato su Linux Hello possono continuare a lavorare con i dati di produzione esistente.

4. Importare i dati temporanei di cui è stata eseguita una copia di backup.

5. Avvia processi/continua l'elaborazione tramite il nuovo cluster di hello.

### <a name="copy-data-toohello-test-environment"></a>Ambiente di test toohello copia dati

Sono presenti molti dati hello toocopy di metodi e i processi, tuttavia hello due illustrati in questa sezione sono hello più semplice metodi toodirectly spostamento file tooa test del cluster.

#### <a name="hdfs-copy"></a>Copia HDFS

Utilizzare hello seguenti dati toocopy passaggi dagli hello produzione cluster toohello il testing cluster. Questi passaggi utilizzano hello `hdfs dfs` utilità che è incluso in HDInsight.

1. Trovare hello storage account e l'impostazione predefinita le informazioni sul contenitore per il cluster esistente. Hello di esempio seguente usa PowerShell tooretrieve queste informazioni:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate un ambiente di test, hello procedura nei cluster basati su Linux creare hello nel documento di HDInsight. Arrestare prima di creare cluster hello e selezionare invece **configurazione facoltativa**.

3. Dal Pannello di configurazione facoltativa hello, selezionare **account di archiviazione collegati**.

4. Selezionare **aggiungere una chiave di archiviazione**e quando richiesto, selezionare l'account di archiviazione hello che è stato restituito da hello script di PowerShell nel passaggio 1. Fare clic su **Seleziona** in ogni pannello. Infine, creare il cluster di hello.

5. Dopo aver creato il cluster hello, connettersi utilizzando tooit **SSH.** Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

6. Dalla sessione SSH hello, utilizzare i seguenti file di comando toocopy da hello collegato storage account toohello nuovo account di archiviazione predefinito hello. Sostituire contenitore con le informazioni sul contenitore hello restituite da PowerShell. Sostituire __ACCOUNT__ con il nome di account hello. Sostituire hello percorso toodata con file di dati tooa percorso hello.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Se non esiste nell'ambiente di test hello struttura di directory hello che contiene dati hello, è possibile creare tramite hello comando seguente:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Hello `-p` switch consente la creazione di hello di tutte le directory nel percorso di hello.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Copia diretta tra i BLOB in Archiviazione di Azure

In alternativa, è opportuno toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet toocopy BLOB tra account di archiviazione all'esterno di HDInsight. Per ulteriori informazioni, vedere la procedura hello toomanage sezione BLOB di Azure tramite Azure PowerShell con l'archiviazione di Azure.

## <a name="client-side-technologies"></a>Tecnologie lato client

Tecnologie lato client, ad esempio [cmdlet di Azure PowerShell](/powershell/azureps-cmdlets-docs), [CLI di Azure](../cli-install-nodejs.md), o hello [.NET SDK per Hadoop](https://hadoopsdk.codeplex.com/) cluster basati su Linux toowork di continuare. Queste tecnologie si basano su REST API che hello uguale in entrambi i tipi del sistema operativo cluster.

## <a name="server-side-technologies"></a>Tecnologie lato server

Hello nella tabella seguente fornisce indicazioni sulla migrazione componenti lato server che sono specifici di Windows.

| Se si usa questa tecnologia... | Eseguire questa operazione... |
| --- | --- |
| **PowerShell** (script sul lato server, incluse le Azioni script usate durante la creazione del cluster) |Riscriverli come script di Bash. Per le azioni script vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md) e [Sviluppo di azioni script con HDInsight basati su Linux](hdinsight-hadoop-script-actions-linux.md). |
| **Interfaccia della riga di comando di Azure** (script lato server) |Mentre hello CLI di Azure è disponibile in Linux, non vengono preinstallato nei nodi head del cluster HDInsight hello. Per ulteriori informazioni sull'installazione hello CLI di Azure, vedere [Introduzione a Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Componenti .NET** |.NET è supportato nei cluster HDInsight basati su Linux tramite [Mono](https://mono-project.com). Per ulteriori informazioni, vedere [soluzioni .NET di eseguire la migrazione basata su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Componenti di Win32 o altre tecnologie esclusive di Windows** |Linee guida dipende dal componente hello o una tecnologia. Potrebbe essere in grado di toofind una versione compatibile con Linux, oppure potrebbe necessario toofind una soluzione alternativa o riscrivere questo componente. |

> [!IMPORTANT]
> gestione di HDInsight Hello SDK non è completamente compatibile con Mono. Non deve essere utilizzato come parte delle soluzioni distribuite cluster HDInsight toohello in questo momento.

## <a name="cluster-creation"></a>Creazione del cluster

Questa sezione illustra le differenze nella creazione del cluster.

### <a name="ssh-user"></a>Utente SSH

Cluster HDInsight basati su Linux usare hello **Secure Shell (SSH)** protocollo i nodi del cluster toohello tooprovide accesso remoto. A differenza dei desktop remoti per i cluster basati Windows, la maggior parte dei client SSH non offrono un'esperienza utente con interfaccia grafica. Al contrario, i client SSH forniscono una riga di comando che consente di comandi toorun nel cluster hello. Alcuni client (ad esempio [MobaXterm](http://mobaxterm.mobatek.net/)) forniscono un visualizzatore di sistema di file con interfaccia grafica nella riga di comando remoto tooa aggiunta.

Durante la creazione del cluster è necessario specificare un utente SSH e una **password** oppure un **certificato di chiave pubblica** per l'autenticazione.

È consigliabile usare il certificato di chiave pubblica perché è più sicuro rispetto alla password. L'autenticazione del certificato funziona, la generazione di una coppia di chiavi pubblica/privata con segno, quindi fornire la chiave pubblica di hello durante la creazione di cluster hello. Durante la connessione server toohello tramite SSH, chiave privata hello client hello fornisce l'autenticazione per la connessione hello.

Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Personalizzazione cluster

**Azioni script** usate con i cluster basati su Linux devono essere scritte nello script Bash. Mentre le azioni Script può essere utilizzate durante la creazione di un cluster, per i cluster basati su Linux possono anche essere utilizzati tooperform personalizzazione dopo che un cluster sia attivo e in esecuzione. Per altre informazioni vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md) e [Sviluppo di azioni script con HDInsight basati su Linux](hdinsight-hadoop-script-actions-linux.md).

Un'altra funzionalità di personalizzazione è **bootstrap**, Per i cluster di Windows, questa funzionalità consente percorso hello toospecify di librerie aggiuntive per l'utilizzo con Hive. Dopo la creazione di cluster, queste librerie sono automaticamente disponibili per l'utilizzo con le query Hive senza hello necessità toouse `ADD JAR`.

funzionalità di Bootstrap Hello per i cluster basati su Linux non fornisce questa funzionalità. Usare invece l'azione script documentata nell'articolo [Aggiungere librerie Hive durante la creazione del cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Reti virtuali

I cluster HDInsight basati su Windows funzionano soltanto con le reti virtuali classiche, mentre i cluster HDInsight basati su Linux richiedono le reti virtuali di gestione risorse. Se si dispone di risorse una rete virtuale classica hello cluster Linux HDInsight è necessario connettersi a, vedere [tooa una rete virtuale classica rete virtuale di gestione risorse di connessione](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Per altre informazioni sui requisiti di configurazione per usare le reti virtuali di Azure con HDInsight, vedere [Estendere le funzionalità di HDInsight usando una rete virtuale](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Gestione e monitoraggio

Molte delle web hello interfacce utente potrebbe essere usata con HDInsight basati su Windows, ad esempio la cronologia processo oppure dell'interfaccia utente Yarn, sono disponibili tramite Ambari. Inoltre, hello Ambari Hive Vista fornisce toorun un modo query Hive tramite il browser. Hello dell'interfaccia utente Web Ambari è disponibile nel cluster di https://CLUSTERNAME.azurehdinsight.net basati su Linux.

Per ulteriori informazioni sull'uso di Ambari, vedere hello seguenti documenti:

* [Web Ambari](hdinsight-hadoop-manage-ambari.md)
* [API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Avvisi di Ambari

Ambari è un sistema di avvisi che possa indicare potenziali problemi con i cluster di hello. Gli avvisi vengono visualizzati come voci rosse o gialle hello Ambari dell'interfaccia utente Web, tuttavia è possibile recuperare anche tramite API REST hello.

> [!IMPORTANT]
> Gli avvisi Ambari indicano che *potrebbe* esserci un problema e non che *è* presente un problema. Ad esempio, un avviso potrebbe indicare che HiveServer2 non è accessibile anche se è possibile accedervi normalmente.
>
> Molti avvisi vengono implementati come query basate su intervalli di tempo nell'ambito di un servizio e attendono una risposta entro un intervallo di tempo specifico. In modo avviso hello non significa necessariamente che il servizio di hello è inattivo, semplicemente che non restituisca risultati entro il periodo di tempo previsto di hello.

È opportuno valutare se un avviso si verifica per molto tempo o se indica problemi dell'utente che erano stati segnalati prima di intervenire.

## <a name="file-system-locations"></a>Percorsi del file system

sistema di file di cluster Linux Hello è disposto in modo diverso rispetto ai cluster HDInsight basati su Windows. Utilizzare i seguenti tabella toofind comunemente utilizzati file hello.

| È necessario toofind... | Si trova... |
| --- | --- |
| Configurazione |`/etc`. Ad esempio, `/etc/hadoop/conf/core-site.xml` |
| File di log |`/var/logs` |
| Hortonworks Data Platform (HDP) |`/usr/hdp`. Esistono due directory si trova in questo caso, una versione di hello corrente HDP e `current`. Hello `current` directory contiene toofiles collegamenti simbolici e directory si trova nella directory numero versione di hello. Hello `current` directory viene fornito come un modo pratico per l'accesso ai file HDP dall'hello numero di versione cambia come hello HDP versione viene aggiornata. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

In generale, se si conosce il nome di hello del file hello, è possibile utilizzare hello comando seguente da un percorso del file hello toofind sessione SSH:

    find / -name FILENAME 2>/dev/null

È anche possibile utilizzare caratteri jolly con nome di file hello. Ad esempio, `find / -name *streaming*.jar 2>/dev/null` restituisce hello percorso tooany file jar contenente parola hello streaming come parte del nome file hello.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig e MapReduce

I carichi di lavoro di Pig e MapReduce sono simili ai cluster basati su Linux. Tuttavia, i cluster HDInsight basati su Linux possono essere creati usando versioni più recenti di Hadoop, Hive e Pig. Queste differenze di versione potrebbero introdurre modifiche nel funzionamento delle soluzioni esistenti. Per ulteriori informazioni sulle versioni di hello dei componenti inclusi in HDInsight, vedere [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md).

HDInsight basato su Linux non offre la funzionalità di desktop remoto. In alternativa, è possibile usare SSH tooremotely connettersi toohello nodi head del cluster. Per ulteriori informazioni, vedere hello seguenti documenti:

* [Usare Hive con SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Usare Pig con SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Usare MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Se si utilizza un metastore Hive esterno, è consigliabile eseguire backup hello metastore prima di utilizzarlo con HDInsight basati su Linux. HDInsight basato su Linux è disponibile nelle versioni più recenti di Hive, che possono presentare problemi di incompatibilità con i metastore creati nelle versioni precedenti.

Hello grafico seguente vengono fornite indicazioni sulla migrazione dei carichi di lavoro di Hive.

| Nel sistema basato su Windows si usa... | Nel sistema basato su Linux si usa... |
| --- | --- |
| **Editor Hive** |[vista Hive in Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez è hello motore di esecuzione predefinito per i cluster basati su Linux, in modo hello imposta l'istruzione non è più necessario. |
| Funzioni definite dall'utente C# | Per informazioni sulla convalida dei componenti di c# con HDInsight basati su Linux, vedere [soluzioni .NET di eseguire la migrazione basata su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD o file di script nel server di hello richiamata come parte di un processo Hive |gli script Bash |
| `hive` dal desktop remoto |Usare [Beeline](hdinsight-hadoop-use-hive-beeline.md) o [Hive da una sessione SSH](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Nel sistema basato su Windows si usa... | Nel sistema basato su Linux si usa... |
| --- | --- |
| Funzioni definite dall'utente C# | Per informazioni sulla convalida dei componenti di c# con HDInsight basati su Linux, vedere [soluzioni .NET di eseguire la migrazione basata su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD o file di script nel server di hello richiamata come parte di un processo Pig |gli script Bash |

### <a name="mapreduce"></a>MapReduce

| Nel sistema basato su Windows si usa... | Nel sistema basato su Linux si usa... |
| --- | --- |
| Componenti di mapping e riduttore C# | Per informazioni sulla convalida dei componenti di c# con HDInsight basati su Linux, vedere [soluzioni .NET di eseguire la migrazione basata su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD o file di script nel server di hello richiamata come parte di un processo Hive |gli script Bash |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Se si utilizza un metastore Oozie esterno, è consigliabile eseguire backup hello metastore prima di utilizzarlo con HDInsight basati su Linux. HDInsight basato su Linux è disponibile nelle versioni più recenti di Oozie, che possono presentare problemi di incompatibilità con i metastore creati nelle versioni precedenti.

I flussi di lavoro di Oozie consentono le azioni shell. Azioni shell utilizzano shell predefinita hello per hello del sistema operativo toorun riga di comando. Se si dispone di Oozie flussi di lavoro che si basano su hello shell di Windows, è necessario riscrivere hello toorely di flussi di lavoro nell'ambiente della shell di Linux hello (Bash). Per ulteriori informazioni sull'uso di azioni shell con Oozie, vedere [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html) (Estensioni dell'azione shell di Oozie).

Se si dispone di flussi di lavoro di Oozie che si basano su applicazioni C# richiamate tramite azioni shell, è necessario convalidare le applicazioni in un ambiente Linux. Per ulteriori informazioni, vedere [soluzioni .NET di eseguire la migrazione basata su tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Nel sistema basato su Windows si usa... | Nel sistema basato su Linux si usa... |
| --- | --- |
| Storm Dashboard |Hello Storm Dashboard non è disponibile. Vedere [le topologie di distribuzione e gestire Storm in HDInsight basati su Linux](hdinsight-storm-deploy-monitor-topology-linux.md) per le topologie toosubmit modi |
| Interfaccia utente di Storm |è disponibile all'indirizzo https://CLUSTERNAME.azurehdinsight.net/stormui Hello Storm UI |
| Visual Studio toocreate, distribuire e gestire le topologie di c# o ibrida |Visual Studio può essere utilizzato toocreate, distribuire e gestire c# (SCP.NET) o topologie ibrida in Storm basati su Linux nel cluster HDInsight creati dopo il 10/28/2016. |

## <a name="hbase"></a>HBase

Nei cluster basati su Linux, è padre di znode hello HBase `/hbase-unsecure`. Impostare questo valore nella configurazione di hello per tutte le applicazioni client Java che utilizzano API Java di HBase nativa.

Vedere [Compilare un'applicazione HBase basata su Java](hdinsight-hbase-build-java-maven.md) per un client di esempio che imposta questo valore.

## <a name="spark"></a>Spark

I cluster Spark non erano disponibili nei cluster Windows durante l'anteprima. GA Spark è disponibile solo con i cluster basati su Linux. Non è un percorso di migrazione da un cluster di Spark basati su Linux basati su Windows Spark anteprima cluster tooa versione.

## <a name="known-issues"></a>Problemi noti

### <a name="azure-data-factory-custom-net-activities"></a>Attività .NET personalizzate in Azure Data Factory

Le attività .NET personalizzate in Azure Data Factory non sono attualmente supportate nei cluster HDInsight basati su Linux. È invece necessario utilizzare una delle seguenti attività personalizzate di metodi tooimplement come parte della pipeline di ADF hello.

* Eseguire le attività .NET nel pool di Azure Batch. Vedere la sezione di servizio collegato di Azure Batch utilizzare hello della [utilizzare attività personalizzate in una pipeline di Data Factory di Azure](../data-factory/data-factory-use-custom-activities.md)
* Implementare l'attività hello come attività MapReduce. Per altre informazioni vedere [Richiamare i programmi MapReduce da Data Factory](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Terminazioni riga

In genere le terminazioni riga nei sistemi basati su Windows usano CRLF, mentre nei sistemi basati su Linux usano LF. Se si produce o si prevede che, dati con terminazioni riga CR/LF, potrebbe essere toowork toomodify hello producer o consumer con terminazione di riga hello LF.

Ad esempio, tramite Azure PowerShell tooquery HDInsight in un cluster basato su Windows restituisce i dati con CR/LF. Hello stessa query con un cluster basato su Linux restituisce LF. È consigliabile testare toosee se terminazioni di riga hello causa un problema con il solutuion prima della migrazione di cluster basati su Linux tooa.

Se si dispone di script che vengono eseguiti direttamente nei nodi di cluster Linux hello, è necessario utilizzare sempre LF come terminazione di riga hello. Se si utilizza CR/LF, è possibile riscontrare errori durante l'esecuzione di script hello in un cluster basato su Linux.

Se si conosce che gli script hello non contengano le stringhe con caratteri CR incorporati, è possibile eseguire bulk terminazioni di riga hello modifica utilizzando uno dei seguenti metodi hello:

* **Prima di caricare cluster toohello**: hello utilizzare seguenti terminazioni di riga hello toochange istruzioni PowerShell dagli tooLF CRLF prima del caricamento del cluster di toohello script hello.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Dopo aver caricato cluster toohello**: il comando seguente di hello di uso da un toohello sessione SSH script hello toomodify di cluster basati su Linux.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su come i cluster HDInsight basati su Linux di toocreate](hdinsight-hadoop-provision-linux-clusters.md)
* [Utilizzare tooHDInsight tooconnect SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gestire un cluster basato su Linux tramite Ambari](hdinsight-hadoop-manage-ambari.md)
