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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="d7e0a-103">Risolvere i problemi di HBase con Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7e0a-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="d7e0a-104">Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload Apache HBase in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="d7e0a-105">Come si eseguono i report dei comandi hbck con più aree non assegnate?</span><span class="sxs-lookup"><span data-stu-id="d7e0a-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="d7e0a-106">Un messaggio di errore comuni che potrebbero essere visualizzati quando si esegue hello `hbase hbck` comando è "più aree mancata assegnazione o fori nella catena di hello delle regioni."</span><span class="sxs-lookup"><span data-stu-id="d7e0a-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="d7e0a-107">In hello UI HBase Master, è possibile visualizzare il numero di hello delle aree che sono non bilanciati tra tutti i server di area.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="d7e0a-108">Quindi, è possibile eseguire `hbase hbck` comando fori toosee nella catena di area hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="d7e0a-109">Fori potrebbero essere causati da aree offline hello, pertanto le assegnazioni di hello correzione prima.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="d7e0a-110">toobring hello stato normale tooa indietro di aree non assegnati, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="d7e0a-111">Accedi toohello cluster HBase di HDInsight utilizzando SSH.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="d7e0a-112">tooconnect con shell ZooKeeper hello, eseguire hello `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="d7e0a-113">Eseguire hello `rmr /hbase/regions-in-transition` comando o hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="d7e0a-114">tooexit da hello `hbase zkcli` della shell, utilizzare hello `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="d7e0a-115">Aprire hello dell'interfaccia utente Ambari Apache e quindi riavviare il servizio di Master HBase Active hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="d7e0a-116">Eseguire hello `hbase hbck` comando nuovamente (senza opzioni).</span><span class="sxs-lookup"><span data-stu-id="d7e0a-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="d7e0a-117">Verificare l'output di hello di questo comando di tooensure che tutte le aree vengono assegnate.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="d7e0a-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Come risolvere i problemi di timeout con i comandi hbck per le assegnazioni di aree</span><span class="sxs-lookup"><span data-stu-id="d7e0a-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="d7e0a-119">Problema</span><span class="sxs-lookup"><span data-stu-id="d7e0a-119">Issue</span></span>

<span data-ttu-id="d7e0a-120">Una possibile causa problemi di timeout quando si utilizza hello `hbck` comando potrebbe essere più aree siano hello "in transizione" dello stato per un lungo periodo.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="d7e0a-121">È possibile visualizzare le aree geografiche come offline nei hello UI HBase Master.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="d7e0a-122">Poiché un numero elevato di aree sta tentando di tootransition, HBase Master potrebbe timeout e toobring non è possibile online tali aree.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-123">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-123">Resolution steps</span></span>

1. <span data-ttu-id="d7e0a-124">Accedi toohello cluster HBase di HDInsight utilizzando SSH.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="d7e0a-125">tooconnect con shell ZooKeeper hello, eseguire hello `hbase zkcli` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="d7e0a-126">Eseguire hello `rmr /hbase/regions-in-transition` o hello `rmr /hbase-unsecure/regions-in-transition` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="d7e0a-127">hello tooexit `hbase zkcli` della shell, utilizzare hello `exit` comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="d7e0a-128">In hello Ambari UI, riavviare il servizio di Master HBase Active hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="d7e0a-129">Eseguire hello `hbase hbck -fixAssignments` nuovo il comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="d7e0a-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Come forzare la disabilitazione della modalità sicura di HDFS in un cluster</span><span class="sxs-lookup"><span data-stu-id="d7e0a-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="d7e0a-131">Problema</span><span class="sxs-lookup"><span data-stu-id="d7e0a-131">Issue</span></span>

<span data-ttu-id="d7e0a-132">Hello locale Hadoop Distributed File System (HDFS) è bloccato in modalità provvisoria nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="d7e0a-133">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="d7e0a-133">Detailed description</span></span>

<span data-ttu-id="d7e0a-134">Questo errore potrebbe essere causato da un errore quando si esegue hello HDFS comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="d7e0a-135">Errore di Hello che si potrebbero verificare quando si tenta di comando hello toorun è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-135">hello error you might see when you try toorun hello command looks like this:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="d7e0a-136">Possibile causa</span><span class="sxs-lookup"><span data-stu-id="d7e0a-136">Probable cause</span></span>

<span data-ttu-id="d7e0a-137">Hello cluster HDInsight è stata ridimensionata tooa molto alcuni nodi.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="d7e0a-138">il numero di Hello di nodi di sotto o chiusura fattore di replica toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-139">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-139">Resolution steps</span></span> 

1. <span data-ttu-id="d7e0a-140">Ottenere lo stato di hello di hello che HDFS su hello HDInsight cluster eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

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
2. <span data-ttu-id="d7e0a-141">È anche possibile controllare l'integrità di hello che HDFS su hello HDInsight cluster utilizzando i seguenti comandi hello hello:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

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

3. <span data-ttu-id="d7e0a-142">Se si determina che non esistono blocchi di mancanti, danneggiati o under-replicati o che possono essere ignorati i blocchi, eseguire hello successivo nodo del nome di comando tootake hello dalla modalità provvisoria:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="d7e0a-143">Come risolvere i problemi di connettività relativi a JDBC o SQLLine con Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="d7e0a-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-144">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-144">Resolution steps</span></span>

<span data-ttu-id="d7e0a-145">tooconnect con Phoenix, è necessario fornire l'indirizzo IP hello di un nodo ZooKeeper attivo.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="d7e0a-146">Verificare che ZooKeeper sqlline.py toowhich servizio sta tentando di hello tooconnect sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="d7e0a-147">Accedi toohello cluster HDInsight tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="d7e0a-148">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="d7e0a-149">È possibile ottenere l'indirizzo IP di hello del nodo ZooKeeper attivo hello da hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="d7e0a-150">Andare troppo**HBase** > **collegamenti rapidi** > **ZK\* (attivo)** > **Zookeeper Info**.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="d7e0a-151">Se hello sqlline.py si connette tooPhoenix e non un limite di timeout, comando che segue hello esecuzione toovalidate hello disponibilità e l'integrità di Phoenix:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="d7e0a-152">Se il comando funziona, non sussistono problemi.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-152">If this command works, there is no issue.</span></span> <span data-ttu-id="d7e0a-153">l'indirizzo IP Hello fornito dall'utente hello potrebbe essere errato.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="d7e0a-154">Tuttavia, se il comando di hello viene sospeso per un periodo di tempo prolungato e quindi viene visualizzato il seguente errore hello, continuare toostep 5.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="d7e0a-155">Eseguire hello seguendo i comandi dalla condizione di hello nodo head (hn0) toodiagnose hello di hello Phoenix sistema. Tabella del catalogo:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="d7e0a-156">comando Hello deve restituire un seguente toohello simile di errore:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="d7e0a-157">Hello Ambari UI, completare hello seguente servizio HMaster hello toorestart di passaggi in tutti i nodi ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="d7e0a-158">In hello **riepilogo** sezione di HBase, andare troppo**HBase** > **Master HBase Active**.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="d7e0a-159">In hello **componenti** sezione, riavviare il servizio di HBase Master hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="d7e0a-160">Ripetere questi passaggi per tutti i rimanenti servizi **Standby HBase Master** (HBase Master in standby).</span><span class="sxs-lookup"><span data-stu-id="d7e0a-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="d7e0a-161">Può richiedere minuti toofive hello Master HBase servizio toostabilize e completare il processo di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="d7e0a-162">Dopo alcuni minuti, ripetere hello sqlline.py comandi tooconfirm tale sistema hello. Tabella del catalogo è attivo e che è possibile eseguire query.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="d7e0a-163">Quando hello del sistema. Tabella del catalogo è toonormal indietro, tooPhoenix problema di connettività hello devono essere risolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="d7e0a-164">Qual è la causa di un server master toofail toostart</span><span class="sxs-lookup"><span data-stu-id="d7e0a-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="d7e0a-165">Errore</span><span class="sxs-lookup"><span data-stu-id="d7e0a-165">Error</span></span> 

<span data-ttu-id="d7e0a-166">Si verifica un errore di ridenominazione atomica.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="d7e0a-167">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="d7e0a-167">Detailed description</span></span>

<span data-ttu-id="d7e0a-168">Durante il processo di avvio di hello, HMaster completa molte operazioni di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="d7e0a-169">Sono inclusi lo spostamento dei dati da zero hello (tmp) una cartella toohello dati.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="d7e0a-170">HMaster prende in considerazione anche hello log write-ahead (WALs) cartella toosee se sono presenti server qualsiasi area che non risponde, e così via.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="d7e0a-171">Durante l'avvio, HMaster esegue un comando `list` di base su tali cartelle.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="d7e0a-172">Se in qualunque momento rileva un file imprevisto in una delle cartelle, HMaster genera un'eccezione e non viene avviato.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="d7e0a-173">Possibile causa</span><span class="sxs-lookup"><span data-stu-id="d7e0a-173">Probable cause</span></span>

<span data-ttu-id="d7e0a-174">Nei registri di server area hello, provare la sequenza temporale hello tooidentify hello creazione dei file e verificare se si è verificato che un arresto anomalo del processo per file di hello hello ora è stato creato.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="d7e0a-175">(Contattare tooassist supporto HBase in questo modo.) In questo modo saranno disponibili meccanismi più affidabili per evitare di incorrere in questo bug e garantire l'arresto normale dei processi.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-176">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-176">Resolution steps</span></span>

<span data-ttu-id="d7e0a-177">Verifica dello stack di chiamate hello e provare la cartella potrebbe essere la causa problema hello toodetermine (ad esempio, potrebbe essere cartella WALs hello o una cartella con estensione tmp hello).</span><span class="sxs-lookup"><span data-stu-id="d7e0a-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="d7e0a-178">Quindi, in Cloud Explorer oppure utilizzando i comandi HDFS effettuato un tentativo toolocate hello problema file.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="d7e0a-179">che è in genere un file \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="d7e0a-180">(hello \*-renamePending.json file è un file journal che usa l'operazione di ridenominazione atomica hello tooimplement nel driver WASB hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="d7e0a-181">Scadenza toobugs in questa implementazione, questi file possono essere rimasti dopo l'arresto del processo e così via.) Forzare l'eliminazione del file in Cloud Explorer o con comandi HDFS.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="d7e0a-182">In questo percorso potrebbe essere talvolta presente anche un file con un nome simile a *$$$.$$$*.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="d7e0a-183">Si dispone di toouse HDFS `ls` questo file di comando toosee; non è possibile visualizzare file hello in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="d7e0a-184">toodelete questo file, utilizzare hello HDFS comando `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="d7e0a-185">Dopo l'esecuzione di questi comandi, HMaster dovrebbe essere avviato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="d7e0a-186">Errore</span><span class="sxs-lookup"><span data-stu-id="d7e0a-186">Error</span></span>

<span data-ttu-id="d7e0a-187">In *hbase: meta* non è elencato alcun indirizzo del server per l'area xxx.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="d7e0a-188">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="d7e0a-188">Detailed description</span></span>

<span data-ttu-id="d7e0a-189">Si potrebbe essere visualizzato un messaggio sul cluster Linux che indica che hello *hbase: meta* tabella non è online.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="d7e0a-190">L'esecuzione di `hbck` potrebbe segnalare che non è stato possibile trovare la tabella hbase: meta con replicaId 0 in alcuna area.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="d7e0a-191">problema di Hello potrebbe essere che HMaster non è stato possibile inizializzare dopo il riavvio di HBase.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="d7e0a-192">In registri HMaster hello, è possibile visualizzare il messaggio hello: "Nessun indirizzo di server elencati in hbase: metadati per l'area hbase: backup \<nome dell'area\>".</span><span class="sxs-lookup"><span data-stu-id="d7e0a-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-193">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-193">Resolution steps</span></span>

1. <span data-ttu-id="d7e0a-194">Nella shell di HBase hello, immettere hello seguenti comandi (modifica i valori effettivi come applicabile):</span><span class="sxs-lookup"><span data-stu-id="d7e0a-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="d7e0a-195">Eliminare hello *hbase: spazio dei nomi* voce.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="d7e0a-196">Questa voce potrebbe non essere lo stesso errore che viene segnalato quando hello hello *hbase: spazio dei nomi* tabella viene analizzata.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="d7e0a-197">toobring di HBase in uno stato in esecuzione, in hello Ambari UI, riavviare il servizio di HMaster Active hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="d7e0a-198">Nella shell di HBase, toobring di tutte le tabelle non in linea, hello eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="d7e0a-199">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d7e0a-199">Additional reading</span></span>

[<span data-ttu-id="d7e0a-200">Nella tabella non è possibile tooprocess hello HBase</span><span class="sxs-lookup"><span data-stu-id="d7e0a-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="d7e0a-201">Errore</span><span class="sxs-lookup"><span data-stu-id="d7e0a-201">Error</span></span>

<span data-ttu-id="d7e0a-202">HMaster timeout con un too"java.io.IOException simile a un'eccezione irreversibile: 300000ms Timedout in attesa per spazio dei nomi tabella toobe assegnato."</span><span class="sxs-lookup"><span data-stu-id="d7e0a-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="d7e0a-203">Descrizione dettagliata</span><span class="sxs-lookup"><span data-stu-id="d7e0a-203">Detailed description</span></span>

<span data-ttu-id="d7e0a-204">Questo problema potrebbe verificarsi se al riavvio dei servizi HMaster sono presenti diverse tabelle e aree che non sono state scaricate.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="d7e0a-205">Il riavvio potrebbe avere esito negativo e verrà visualizzato hello che precede il messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="d7e0a-206">Possibile causa</span><span class="sxs-lookup"><span data-stu-id="d7e0a-206">Probable cause</span></span>

<span data-ttu-id="d7e0a-207">Si tratta di un problema noto con hello HMaster servizio.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="d7e0a-208">Le attività di avvio generali del cluster possono richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="d7e0a-209">Arresta HMaster perché nella tabella hello dello spazio dei nomi non è ancora assegnata.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="d7e0a-210">Questo si verifica solo in scenari in cui è presente una grande quantità di dati non scaricati e un timeout di cinque minuti non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-211">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-211">Resolution steps</span></span>

1. <span data-ttu-id="d7e0a-212">In hello Ambari UI, andare troppo**HBase** > **configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="d7e0a-213">Nel file hbase-Site.XML personalizzata hello aggiungere hello seguente impostazione:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="d7e0a-214">Riavviare i servizi necessario hello (HMaster e possibilmente altri servizi di HBase).</span><span class="sxs-lookup"><span data-stu-id="d7e0a-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="d7e0a-215">Qual è la causa di un errore di riavvio in un server di area?</span><span class="sxs-lookup"><span data-stu-id="d7e0a-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="d7e0a-216">Problema</span><span class="sxs-lookup"><span data-stu-id="d7e0a-216">Issue</span></span>

<span data-ttu-id="d7e0a-217">È possibile prevenire un errore di avvio in un server di area seguendo le procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="d7e0a-218">Si consiglia sospendere attività carichi di lavoro per pianificare i server di toorestart HBase area.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="d7e0a-219">Se un'applicazione continua tooconnect con i server area quando l'istruzione shutdown è in corso, l'operazione di riavvio hello area server sarà più lento da alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="d7e0a-220">Inoltre, è toofirst una buona idea scaricamento di che tutte le tabelle di hello.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="d7e0a-221">Per informazioni di riferimento sul tooflush tabelle, vedere [HDInsight HBase: come cluster HBase di hello tooimprove riavviare ora rimuovendo tabelle](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="d7e0a-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="d7e0a-222">Se si avvia l'operazione di riavvio hello nei server di HBase area da hello Ambari UI, vengono immediatamente visualizzati che server area hello è arrestato, ma non riavviare immediatamente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="d7e0a-223">Ecco che cosa avviene in background hello:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="d7e0a-224">l'agente Ambari Hello invia un arresto richiesta toohello regione del server.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="d7e0a-225">Hello Ambari agente attende 30 secondi per hello area server tooshut verso il basso normalmente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="d7e0a-226">Se l'applicazione continua a tooconnect con server area hello, hello server non verrà arrestato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="d7e0a-227">timeout di 30 secondi Hello scade prima che si verifica l'arresto.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="d7e0a-228">Dopo 30 secondi, agente Ambari hello invia un force-kill (`kill -9`) server area toohello di comando.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="d7e0a-229">È possibile vedere questo nel log dell'agente di ambari hello (nella directory log//var hello del nodo rispettivo lavoro hello):</span><span class="sxs-lookup"><span data-stu-id="d7e0a-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

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
<span data-ttu-id="d7e0a-230">A causa dell'arresto improvviso hello, porta hello associata al processo hello potrebbe non essere rilasciata, anche se hello area server processo viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="d7e0a-231">Questa situazione può causare tooan AddressBindException all'avvio di hello area server, come illustrato nell'hello seguenti registri.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="d7e0a-232">È possibile verificare questa nell'area hello-server.log nella directory /var/log/hbase hello nei nodi di lavoro hello in cui il server di area hello ha esito negativo toostart.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

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

### <a name="resolution-steps"></a><span data-ttu-id="d7e0a-233">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="d7e0a-233">Resolution steps</span></span>

1. <span data-ttu-id="d7e0a-234">Provare tooreduce hello carico sui server di area hello HBase prima di iniziare il riavvio.</span><span class="sxs-lookup"><span data-stu-id="d7e0a-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="d7e0a-235">In alternativa (se non consente il passaggio 1), comandi area di riavvio toomanually provare i server in nodi di lavoro hello utilizzando hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7e0a-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

