---
title: aaaTroubleshoot HBase tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'utilizzo di HBase e Azure HDInsight.
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Risolvere i problemi di HBase con Azure HDInsight

Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload Apache HBase in Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Come si eseguono i report dei comandi hbck con più aree non assegnate?

Un messaggio di errore comuni che potrebbero essere visualizzati quando si esegue hello `hbase hbck` comando è "più aree mancata assegnazione o fori nella catena di hello delle regioni."

In hello UI HBase Master, è possibile visualizzare il numero di hello delle aree che sono non bilanciati tra tutti i server di area. Quindi, è possibile eseguire `hbase hbck` comando fori toosee nella catena di area hello.

Fori potrebbero essere causati da aree offline hello, pertanto le assegnazioni di hello correzione prima. 

toobring hello stato normale tooa indietro di aree non assegnati, completare hello alla procedura seguente:

1. Accedi toohello cluster HBase di HDInsight utilizzando SSH.
2. tooconnect con shell ZooKeeper hello, eseguire hello `hbase zkcli` comando.
3. Eseguire hello `rmr /hbase/regions-in-transition` comando o hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. tooexit da hello `hbase zkcli` della shell, utilizzare hello `exit` comando.
5. Aprire hello dell'interfaccia utente Ambari Apache e quindi riavviare il servizio di Master HBase Active hello.
6. Eseguire hello `hbase hbck` comando nuovamente (senza opzioni). Verificare l'output di hello di questo comando di tooensure che tutte le aree vengono assegnate.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Come risolvere i problemi di timeout con i comandi hbck per le assegnazioni di aree

### <a name="issue"></a>Problema

Una possibile causa problemi di timeout quando si utilizza hello `hbck` comando potrebbe essere più aree siano hello "in transizione" dello stato per un lungo periodo. È possibile visualizzare le aree geografiche come offline nei hello UI HBase Master. Poiché un numero elevato di aree sta tentando di tootransition, HBase Master potrebbe timeout e toobring non è possibile online tali aree.

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Accedi toohello cluster HBase di HDInsight utilizzando SSH.
2. tooconnect con shell ZooKeeper hello, eseguire hello `hbase zkcli` comando.
3. Eseguire hello `rmr /hbase/regions-in-transition` o hello `rmr /hbase-unsecure/regions-in-transition` comando.
4. hello tooexit `hbase zkcli` della shell, utilizzare hello `exit` comando.
5. In hello Ambari UI, riavviare il servizio di Master HBase Active hello.
6. Eseguire hello `hbase hbck -fixAssignments` nuovo il comando.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Come forzare la disabilitazione della modalità sicura di HDFS in un cluster

### <a name="issue"></a>Problema

Hello locale Hadoop Distributed File System (HDFS) è bloccato in modalità provvisoria nel cluster HDInsight hello.

### <a name="detailed-description"></a>Descrizione dettagliata

Questo errore potrebbe essere causato da un errore quando si esegue hello HDFS comando seguente:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Errore di Hello che si potrebbero verificare quando si tenta di comando hello toorun è simile al seguente:

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a>Possibile causa

Hello cluster HDInsight è stata ridimensionata tooa molto alcuni nodi. il numero di Hello di nodi di sotto o chiusura fattore di replica toohello HDFS.

### <a name="resolution-steps"></a>Procedura per la risoluzione 

1. Ottenere lo stato di hello di hello che HDFS su hello HDInsight cluster eseguendo hello seguenti comandi:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. È anche possibile controllare l'integrità di hello che HDFS su hello HDInsight cluster utilizzando i seguenti comandi hello hello:

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. Se si determina che non esistono blocchi di mancanti, danneggiati o under-replicati o che possono essere ignorati i blocchi, eseguire hello successivo nodo del nome di comando tootake hello dalla modalità provvisoria:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Come risolvere i problemi di connettività relativi a JDBC o SQLLine con Apache Phoenix

### <a name="resolution-steps"></a>Procedura per la risoluzione

tooconnect con Phoenix, è necessario fornire l'indirizzo IP hello di un nodo ZooKeeper attivo. Verificare che ZooKeeper sqlline.py toowhich servizio sta tentando di hello tooconnect sia in esecuzione.
1. Accedi toohello cluster HDInsight tramite SSH.
2. Immettere hello comando seguente:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > È possibile ottenere l'indirizzo IP di hello del nodo ZooKeeper attivo hello da hello Ambari UI. Andare troppo**HBase** > **collegamenti rapidi** > **ZK\* (attivo)** > **Zookeeper Info**. 

3. Se hello sqlline.py si connette tooPhoenix e non un limite di timeout, comando che segue hello esecuzione toovalidate hello disponibilità e l'integrità di Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. Se il comando funziona, non sussistono problemi. l'indirizzo IP Hello fornito dall'utente hello potrebbe essere errato. Tuttavia, se il comando di hello viene sospeso per un periodo di tempo prolungato e quindi viene visualizzato il seguente errore hello, continuare toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Eseguire hello seguendo i comandi dalla condizione di hello nodo head (hn0) toodiagnose hello di hello Phoenix sistema. Tabella del catalogo:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   comando Hello deve restituire un seguente toohello simile di errore: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Hello Ambari UI, completare hello seguente servizio HMaster hello toorestart di passaggi in tutti i nodi ZooKeeper:

    1. In hello **riepilogo** sezione di HBase, andare troppo**HBase** > **Master HBase Active**. 
    2. In hello **componenti** sezione, riavviare il servizio di HBase Master hello.
    3. Ripetere questi passaggi per tutti i rimanenti servizi **Standby HBase Master** (HBase Master in standby). 

Può richiedere minuti toofive hello Master HBase servizio toostabilize e completare il processo di ripristino hello. Dopo alcuni minuti, ripetere hello sqlline.py comandi tooconfirm tale sistema hello. Tabella del catalogo è attivo e che è possibile eseguire query. 

Quando hello del sistema. Tabella del catalogo è toonormal indietro, tooPhoenix problema di connettività hello devono essere risolti automaticamente.


## <a name="what-causes-a-master-server-toofail-toostart"></a>Qual è la causa di un server master toofail toostart

### <a name="error"></a>Errore 

Si verifica un errore di ridenominazione atomica.

### <a name="detailed-description"></a>Descrizione dettagliata

Durante il processo di avvio di hello, HMaster completa molte operazioni di inizializzazione. Sono inclusi lo spostamento dei dati da zero hello (tmp) una cartella toohello dati. HMaster prende in considerazione anche hello log write-ahead (WALs) cartella toosee se sono presenti server qualsiasi area che non risponde, e così via. 

Durante l'avvio, HMaster esegue un comando `list` di base su tali cartelle. Se in qualunque momento rileva un file imprevisto in una delle cartelle, HMaster genera un'eccezione e non viene avviato.  

### <a name="probable-cause"></a>Possibile causa

Nei registri di server area hello, provare la sequenza temporale hello tooidentify hello creazione dei file e verificare se si è verificato che un arresto anomalo del processo per file di hello hello ora è stato creato. (Contattare tooassist supporto HBase in questo modo.) In questo modo saranno disponibili meccanismi più affidabili per evitare di incorrere in questo bug e garantire l'arresto normale dei processi.

### <a name="resolution-steps"></a>Procedura per la risoluzione

Verifica dello stack di chiamate hello e provare la cartella potrebbe essere la causa problema hello toodetermine (ad esempio, potrebbe essere cartella WALs hello o una cartella con estensione tmp hello). Quindi, in Cloud Explorer oppure utilizzando i comandi HDFS effettuato un tentativo toolocate hello problema file. che è in genere un file \*-renamePending.json. (hello \*-renamePending.json file è un file journal che usa l'operazione di ridenominazione atomica hello tooimplement nel driver WASB hello. Scadenza toobugs in questa implementazione, questi file possono essere rimasti dopo l'arresto del processo e così via.) Forzare l'eliminazione del file in Cloud Explorer o con comandi HDFS. 

In questo percorso potrebbe essere talvolta presente anche un file con un nome simile a *$$$.$$$*. Si dispone di toouse HDFS `ls` questo file di comando toosee; non è possibile visualizzare file hello in Cloud Explorer. toodelete questo file, utilizzare hello HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Dopo l'esecuzione di questi comandi, HMaster dovrebbe essere avviato immediatamente. 

### <a name="error"></a>Errore

In *hbase: meta* non è elencato alcun indirizzo del server per l'area xxx.

### <a name="detailed-description"></a>Descrizione dettagliata

Si potrebbe essere visualizzato un messaggio sul cluster Linux che indica che hello *hbase: meta* tabella non è online. L'esecuzione di `hbck` potrebbe segnalare che non è stato possibile trovare la tabella hbase: meta con replicaId 0 in alcuna area. problema di Hello potrebbe essere che HMaster non è stato possibile inizializzare dopo il riavvio di HBase. In registri HMaster hello, è possibile visualizzare il messaggio hello: "Nessun indirizzo di server elencati in hbase: metadati per l'area hbase: backup \<nome dell'area\>".  

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Nella shell di HBase hello, immettere hello seguenti comandi (modifica i valori effettivi come applicabile):  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Eliminare hello *hbase: spazio dei nomi* voce. Questa voce potrebbe non essere lo stesso errore che viene segnalato quando hello hello *hbase: spazio dei nomi* tabella viene analizzata.

3. toobring di HBase in uno stato in esecuzione, in hello Ambari UI, riavviare il servizio di HMaster Active hello.  

4. Nella shell di HBase, toobring di tutte le tabelle non in linea, hello eseguire hello comando seguente:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Informazioni aggiuntive

[Nella tabella non è possibile tooprocess hello HBase](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Errore

HMaster timeout con un too"java.io.IOException simile a un'eccezione irreversibile: 300000ms Timedout in attesa per spazio dei nomi tabella toobe assegnato."

### <a name="detailed-description"></a>Descrizione dettagliata

Questo problema potrebbe verificarsi se al riavvio dei servizi HMaster sono presenti diverse tabelle e aree che non sono state scaricate. Il riavvio potrebbe avere esito negativo e verrà visualizzato hello che precede il messaggio di errore.  

### <a name="probable-cause"></a>Possibile causa

Si tratta di un problema noto con hello HMaster servizio. Le attività di avvio generali del cluster possono richiedere molto tempo. Arresta HMaster perché nella tabella hello dello spazio dei nomi non è ancora assegnata. Questo si verifica solo in scenari in cui è presente una grande quantità di dati non scaricati e un timeout di cinque minuti non è sufficiente.
  
### <a name="resolution-steps"></a>Procedura per la risoluzione

1. In hello Ambari UI, andare troppo**HBase** > **configurazioni**. Nel file hbase-Site.XML personalizzata hello aggiungere hello seguente impostazione: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Riavviare i servizi necessario hello (HMaster e possibilmente altri servizi di HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Qual è la causa di un errore di riavvio in un server di area?

### <a name="issue"></a>Problema

È possibile prevenire un errore di avvio in un server di area seguendo le procedure consigliate. Si consiglia sospendere attività carichi di lavoro per pianificare i server di toorestart HBase area. Se un'applicazione continua tooconnect con i server area quando l'istruzione shutdown è in corso, l'operazione di riavvio hello area server sarà più lento da alcuni minuti. Inoltre, è toofirst una buona idea scaricamento di che tutte le tabelle di hello. Per informazioni di riferimento sul tooflush tabelle, vedere [HDInsight HBase: come cluster HBase di hello tooimprove riavviare ora rimuovendo tabelle](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Se si avvia l'operazione di riavvio hello nei server di HBase area da hello Ambari UI, vengono immediatamente visualizzati che server area hello è arrestato, ma non riavviare immediatamente. 

Ecco che cosa avviene in background hello: 

1. l'agente Ambari Hello invia un arresto richiesta toohello regione del server.
2. Hello Ambari agente attende 30 secondi per hello area server tooshut verso il basso normalmente. 
3. Se l'applicazione continua a tooconnect con server area hello, hello server non verrà arrestato immediatamente. timeout di 30 secondi Hello scade prima che si verifica l'arresto. 
4. Dopo 30 secondi, agente Ambari hello invia un force-kill (`kill -9`) server area toohello di comando. È possibile vedere questo nel log dell'agente di ambari hello (nella directory log//var hello del nodo rispettivo lavoro hello):

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
A causa dell'arresto improvviso hello, porta hello associata al processo hello potrebbe non essere rilasciata, anche se hello area server processo viene arrestato. Questa situazione può causare tooan AddressBindException all'avvio di hello area server, come illustrato nell'hello seguenti registri. È possibile verificare questa nell'area hello-server.log nella directory /var/log/hbase hello nei nodi di lavoro hello in cui il server di area hello ha esito negativo toostart. 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Provare tooreduce hello carico sui server di area hello HBase prima di iniziare il riavvio. 
2. In alternativa (se non consente il passaggio 1), comandi area di riavvio toomanually provare i server in nodi di lavoro hello utilizzando hello seguenti:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

