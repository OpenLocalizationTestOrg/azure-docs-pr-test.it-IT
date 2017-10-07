---
title: esegue il dump di heap aaaEnable per i servizi Hadoop in HDInsight - Azure | Documenti Microsoft
description: Abilitare i dump dell'heap per i servizi Hadoop dai cluster HDInsight basati su Linux per il debug e l'analisi.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="a66fe-103">Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="a66fe-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="a66fe-104">Dump dell'heap contengono uno snapshot di memoria dell'applicazione hello, inclusi i valori di hello delle variabili in fase di hello dump hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a66fe-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="a66fe-105">Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a66fe-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a66fe-106">Hello passaggi descritti in questo documento funzionano solo con i cluster HDInsight che utilizzano Linux.</span><span class="sxs-lookup"><span data-stu-id="a66fe-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="a66fe-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a66fe-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a66fe-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a66fe-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a66fe-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="a66fe-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="a66fe-110">È possibile abilitare dump dell'heap per hello seguenti servizi:</span><span class="sxs-lookup"><span data-stu-id="a66fe-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="a66fe-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="a66fe-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="a66fe-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="a66fe-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="a66fe-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="a66fe-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="a66fe-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="a66fe-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="a66fe-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="a66fe-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="a66fe-116">È anche possibile abilitare i dump di heap per la mappa hello e ridurre i processi eseguiti da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a66fe-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="a66fe-117"><a name="configuration"></a>Informazioni sulla configurazione dei dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="a66fe-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="a66fe-118">Dump dell'heap sono abilitati per il passaggio di opzioni (talvolta nota anche come opts, o parametri) toohello JVM quando un servizio viene avviato.</span><span class="sxs-lookup"><span data-stu-id="a66fe-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="a66fe-119">Per la maggior parte dei servizi Hadoop, è possibile modificare queste opzioni hello shell script utilizzato toostart hello servizio toopass.</span><span class="sxs-lookup"><span data-stu-id="a66fe-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="a66fe-120">In ogni script è presente un'esportazione per  **\* \_OPTS**, che contiene le opzioni di hello passato toohello JVM.</span><span class="sxs-lookup"><span data-stu-id="a66fe-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="a66fe-121">Ad esempio, in hello **hadoop env.sh** riga hello che inizia con, script `export HADOOP_NAMENODE_OPTS=` contiene le opzioni di hello per hello NameNode servizio.</span><span class="sxs-lookup"><span data-stu-id="a66fe-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="a66fe-122">Eseguire il mapping e ridurre i processi sono leggermente diversi, perché queste operazioni sono un processo figlio di hello servizio MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a66fe-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="a66fe-123">Ogni mapping o ridurre il processo viene eseguito in un contenitore figlio e sono presenti due voci che contengono le opzioni di JVM hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="a66fe-124">Entrambi sono contenuti in **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="a66fe-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="a66fe-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="a66fe-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="a66fe-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="a66fe-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="a66fe-127">È consigliabile con Ambari toomodify entrambi hello script e le impostazioni di mapred-Site.XML, come Ambari gestiscono la replica delle modifiche tra i nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="a66fe-128">Vedere hello [Ambari utilizzando](#using-ambari) sezione per i passaggi specifici.</span><span class="sxs-lookup"><span data-stu-id="a66fe-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="a66fe-129">Abilitare i dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="a66fe-129">Enable heap dumps</span></span>

<span data-ttu-id="a66fe-130">Hello opzione seguente consente il dump di heap quando si verifica un OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="a66fe-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="a66fe-131">Hello  **+**  indica che questa opzione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="a66fe-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="a66fe-132">valore predefinito di Hello è disabled.</span><span class="sxs-lookup"><span data-stu-id="a66fe-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="a66fe-133">Dump dell'heap non sono abilitati per i servizi Hadoop in HDInsight per impostazione predefinita, come i file di dump hello possono essere di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a66fe-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="a66fe-134">Se li si abilita per la risoluzione dei problemi, tenere presente toodisable li dopo avere riprodotto hello problema e i file di dump hello raccolti.</span><span class="sxs-lookup"><span data-stu-id="a66fe-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="a66fe-135">Percorso dei dump</span><span class="sxs-lookup"><span data-stu-id="a66fe-135">Dump location</span></span>

<span data-ttu-id="a66fe-136">Hello percorso predefinito file di dump hello è directory di lavoro corrente hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="a66fe-137">È possibile controllare dove hello file verrà archiviati utilizzando hello seguente opzione:</span><span class="sxs-lookup"><span data-stu-id="a66fe-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="a66fe-138">Ad esempio, usando `-XX:HeapDumpPath=/tmp` provoca hello dump toobe archiviato nella directory /tmp hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="a66fe-139">Script</span><span class="sxs-lookup"><span data-stu-id="a66fe-139">Scripts</span></span>

<span data-ttu-id="a66fe-140">È anche possibile generare uno script quando si verifica un **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="a66fe-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="a66fe-141">Ad esempio, attivare una notifica per sapere di tale errore hello si è verificato.</span><span class="sxs-lookup"><span data-stu-id="a66fe-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="a66fe-142">Seguente hello utilizzare opzione tootrigger uno script in un __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="a66fe-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="a66fe-143">Poiché Hadoop è un sistema distribuito, qualsiasi script utilizzato deve essere inserito in tutti i nodi cluster hello eseguito sul servizio hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="a66fe-144">script Hello deve inoltre essere in una posizione accessibile da hello account hello viene eseguito il servizio come ed è necessario fornire le autorizzazioni di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a66fe-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="a66fe-145">Ad esempio, è preferibile script toostore in `/usr/local/bin` e utilizzare `chmod go+rx /usr/local/bin/filename.sh` toogrant autorizzazioni read ed execute.</span><span class="sxs-lookup"><span data-stu-id="a66fe-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="a66fe-146">Uso di Ambari</span><span class="sxs-lookup"><span data-stu-id="a66fe-146">Using Ambari</span></span>

<span data-ttu-id="a66fe-147">configurazione di hello toomodify per un servizio, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a66fe-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="a66fe-148">Aprire hello Ambari web dell'interfaccia utente per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a66fe-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="a66fe-149">URL di Hello è https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a66fe-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="a66fe-150">Quando richiesto, eseguire l'autenticazione del sito toohello utilizzando un nome di account hello HTTP (impostazione predefinita: amministratore) e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a66fe-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a66fe-151">Potrebbero essere richieste una seconda volta da Ambari hello nome di utente e password.</span><span class="sxs-lookup"><span data-stu-id="a66fe-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="a66fe-152">In questo caso, immettere hello stesso nome di account e password</span><span class="sxs-lookup"><span data-stu-id="a66fe-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="a66fe-153">Utilizzando l'elenco di hello di hello sinistra, selezionare l'area del servizio hello desiderato toomodify.</span><span class="sxs-lookup"><span data-stu-id="a66fe-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="a66fe-154">Ad esempio, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="a66fe-154">For example, **HDFS**.</span></span> <span data-ttu-id="a66fe-155">Nell'area centrale hello selezionare hello **configurazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="a66fe-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Immagine dell'interfaccia Web di Ambari con la scheda HDFS Configs selezionata](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="a66fe-157">Utilizzo di hello **filtro...**  voce, immettere **opts**.</span><span class="sxs-lookup"><span data-stu-id="a66fe-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="a66fe-158">Vengono visualizzati solo gli elementi che contengono questo testo.</span><span class="sxs-lookup"><span data-stu-id="a66fe-158">Only items containing this text are displayed.</span></span>

    ![Elenco filtrato](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="a66fe-160">Trovare hello  **\* \_OPTS** voce per il servizio di hello tooenable dump di heap per desiderato e aggiungere opzioni hello desidera tooenable.</span><span class="sxs-lookup"><span data-stu-id="a66fe-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="a66fe-161">Nella seguente immagine di hello, ho aggiunto `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** voce:</span><span class="sxs-lookup"><span data-stu-id="a66fe-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="a66fe-163">Quando abilitare i dump di heap per hello eseguire il mapping o ridurre il processo figlio, cercare i campi di hello denominati **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="a66fe-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="a66fe-164">Hello utilizzare **salvare** pulsante modifiche hello toosave.</span><span class="sxs-lookup"><span data-stu-id="a66fe-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="a66fe-165">È possibile immettere una breve nota che descrive le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="a66fe-166">Una volta hello modifiche sono state applicate, hello **richiesto riavvio** viene visualizzata l'icona accanto a uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="a66fe-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![icona restart required e pulsante restart](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="a66fe-168">Selezionare ogni servizio che richiede un riavvio e utilizzare hello **azioni servizio** pulsante troppo**attivare la modalità di manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="a66fe-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="a66fe-169">Modalità di manutenzione impedisce avvisi vengono generati dal servizio hello dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="a66fe-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Menu Turn on maintenance mode](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="a66fe-171">Dopo aver abilitato la modalità di manutenzione, utilizzare hello **riavviare** pulsante per il servizio hello troppo**riavviare effettuati tutti**</span><span class="sxs-lookup"><span data-stu-id="a66fe-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Voce Restart All Affected](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="a66fe-173">le voci per hello Hello **riavviare** pulsante può essere diverso per altri servizi.</span><span class="sxs-lookup"><span data-stu-id="a66fe-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="a66fe-174">Una volta hello servizi siano stati riavviati, utilizzare hello **azioni servizio** pulsante troppo**attivare la modalità manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="a66fe-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="a66fe-175">Questo tooresume Ambari monitoraggio per gli avvisi per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="a66fe-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

