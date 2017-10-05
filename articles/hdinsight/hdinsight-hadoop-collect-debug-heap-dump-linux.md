---
title: Abilitare i dump dell'heap per i servizi Hadoop in HDInsight - Azure | Microsoft Docs
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
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="4212c-103">Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux</span><span class="sxs-lookup"><span data-stu-id="4212c-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="4212c-104">I dump dell'heap includono uno snapshot della memoria dell'applicazione, ad esempio i valori delle variabili al momento della creazione del dump.</span><span class="sxs-lookup"><span data-stu-id="4212c-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="4212c-105">Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4212c-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4212c-106">I passaggi descritti in questo documento funzionano solo con i cluster HDInsight che usano Linux.</span><span class="sxs-lookup"><span data-stu-id="4212c-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="4212c-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4212c-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4212c-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4212c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="4212c-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="4212c-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="4212c-110">È possibile abilitare dump dell'heap per i servizi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4212c-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="4212c-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="4212c-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="4212c-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="4212c-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="4212c-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="4212c-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="4212c-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="4212c-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="4212c-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="4212c-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="4212c-116">È inoltre possibile abilitare dump dell'heap per la mappa e ridurre i processi eseguiti da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4212c-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="4212c-117"><a name="configuration"></a>Informazioni sulla configurazione dei dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="4212c-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="4212c-118">I dump dell'heap vengono abilitati mediante il passaggio di opzioni (talvolta noto come parametri) a JVM quando viene avviato un servizio.</span><span class="sxs-lookup"><span data-stu-id="4212c-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="4212c-119">Per la maggior parte dei servizi Hadoop è possibile modificare lo script della shell usato per avviare il servizio per passare queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="4212c-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="4212c-120">In ogni script è presente un'esportazione per **\*\_OPTS**, che contiene le opzioni passate a JVM.</span><span class="sxs-lookup"><span data-stu-id="4212c-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="4212c-121">Ad esempio, nello script **hadoop-env.sh**, la riga che inizia con `export HADOOP_NAMENODE_OPTS=` contiene le opzioni per il servizio NameNode.</span><span class="sxs-lookup"><span data-stu-id="4212c-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="4212c-122">I processi di mapping e riduzione sono leggermente diversi, in quanto queste operazioni sono processi figlio del servizio MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4212c-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="4212c-123">Ogni processo di mapping o riduzione viene eseguito in un contenitore figlio e ci sono due elementi che contengono le opzioni di JVM.</span><span class="sxs-lookup"><span data-stu-id="4212c-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="4212c-124">Entrambi sono contenuti in **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="4212c-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="4212c-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="4212c-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="4212c-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="4212c-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="4212c-127">È consigliabile usare Ambari per modificare gli script e le impostazioni di mapred-site.xml, in quanto Ambari gestisce la replica delle modifiche tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="4212c-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="4212c-128">Per i passaggi specifici, vedere la sezione [Uso di Ambari](#using-ambari) .</span><span class="sxs-lookup"><span data-stu-id="4212c-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="4212c-129">Abilitare i dump dell'heap</span><span class="sxs-lookup"><span data-stu-id="4212c-129">Enable heap dumps</span></span>

<span data-ttu-id="4212c-130">L'opzione seguente abilita il dump dell'heap quando si verifica un OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="4212c-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="4212c-131">**+** indica che l'opzione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="4212c-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="4212c-132">L'impostazione predefinita è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="4212c-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="4212c-133">I dump dell'heap non sono abilitati per i servizi Hadoop in HDInsight per impostazione predefinita, perché i file di dump possono essere di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4212c-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="4212c-134">Se li si abilita per la risoluzione dei problemi, ricordarsi di disabilitarli dopo aver riprodotto il problema e raccolto i file di dump.</span><span class="sxs-lookup"><span data-stu-id="4212c-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="4212c-135">Percorso dei dump</span><span class="sxs-lookup"><span data-stu-id="4212c-135">Dump location</span></span>

<span data-ttu-id="4212c-136">Il percorso predefinito per il file di dump è la directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="4212c-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="4212c-137">È possibile controllare dove viene archiviato il file usando l'opzione seguente:</span><span class="sxs-lookup"><span data-stu-id="4212c-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="4212c-138">Ad esempio, se si usa `-XX:HeapDumpPath=/tmp`, il dump viene archiviato nella directory /tmp.</span><span class="sxs-lookup"><span data-stu-id="4212c-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="4212c-139">Script</span><span class="sxs-lookup"><span data-stu-id="4212c-139">Scripts</span></span>

<span data-ttu-id="4212c-140">È anche possibile generare uno script quando si verifica un **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="4212c-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="4212c-141">Ad esempio, attivando una notifica per sapere che si è verificato l'errore.</span><span class="sxs-lookup"><span data-stu-id="4212c-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="4212c-142">Usare l'opzione seguente per attivare uno script su un __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="4212c-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="4212c-143">Poiché Hadoop è un sistema distribuito, tutti gli script usati devono essere posizionati in tutti i nodi del cluster in cui viene eseguito il servizio.</span><span class="sxs-lookup"><span data-stu-id="4212c-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="4212c-144">Lo script deve anche trovarsi in un percorso accessibile dall'account con cui viene eseguito il servizio e deve fornire autorizzazioni di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4212c-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="4212c-145">Ad esempio, è possibile archiviare gli script in `/usr/local/bin` e usare `chmod go+rx /usr/local/bin/filename.sh` per concedere autorizzazioni di lettura ed esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4212c-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="4212c-146">Uso di Ambari</span><span class="sxs-lookup"><span data-stu-id="4212c-146">Using Ambari</span></span>

<span data-ttu-id="4212c-147">Per modificare la configurazione di un servizio, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4212c-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="4212c-148">Aprire l'interfaccia utente Web di Ambari per il cluster.</span><span class="sxs-lookup"><span data-stu-id="4212c-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="4212c-149">L'URL è https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4212c-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="4212c-150">Quando richiesto, eseguire l'autenticazione al sito usando il nome dell'account HTTP (impostazione predefinita: admin) e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="4212c-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4212c-151">È possibile che Ambari richieda il nome utente e la password una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="4212c-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="4212c-152">In questo caso, immettere lo stesso nome dell'account e la stessa password.</span><span class="sxs-lookup"><span data-stu-id="4212c-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="4212c-153">Usando l'elenco a sinistra, selezionare l'area del servizio da modificare.</span><span class="sxs-lookup"><span data-stu-id="4212c-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="4212c-154">Ad esempio, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="4212c-154">For example, **HDFS**.</span></span> <span data-ttu-id="4212c-155">Nell'area centrale selezionare la scheda **Configs** .</span><span class="sxs-lookup"><span data-stu-id="4212c-155">In the center area, select the **Configs** tab.</span></span>

    ![Immagine dell'interfaccia Web di Ambari con la scheda HDFS Configs selezionata](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="4212c-157">Usando la voce **Filter...** immettere **opts**.</span><span class="sxs-lookup"><span data-stu-id="4212c-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="4212c-158">Vengono visualizzati solo gli elementi che contengono questo testo.</span><span class="sxs-lookup"><span data-stu-id="4212c-158">Only items containing this text are displayed.</span></span>

    ![Elenco filtrato](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="4212c-160">Trovare la voce **\*\_OPTS** per il servizio per cui si vogliono abilitare i dump dell'heap e aggiungere le opzioni da abilitare.</span><span class="sxs-lookup"><span data-stu-id="4212c-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="4212c-161">Nella figura seguente è stato aggiunto `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` alla voce **HADOOP\_NAMENODE\_OPTS**:</span><span class="sxs-lookup"><span data-stu-id="4212c-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="4212c-163">Quando si abilitato i dump dell'heap per il processo figlio di mapping o riduzione, si cercano i campi denominati **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="4212c-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="4212c-164">Fare clic sul pulsante **Save** per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="4212c-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="4212c-165">Sarà possibile immettere una breve nota che descrive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4212c-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="4212c-166">Dopo avere applicato le modifiche, viene visualizzata l'icona **Restart required** accanto a uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="4212c-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![icona restart required e pulsante restart](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="4212c-168">Selezionare ogni servizio che richiede un riavvio e usare il pulsante **Service Actions** per **Disattivare la modalità di manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="4212c-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="4212c-169">La modalità di manutenzione impedisce che vengano generati avvisi quando si riavvia questo servizio.</span><span class="sxs-lookup"><span data-stu-id="4212c-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Menu Turn on maintenance mode](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="4212c-171">Dopo aver abilitato la modalità di manutenzione, usare il pulsante **Restart** per il servizio per **Restart All Effected**</span><span class="sxs-lookup"><span data-stu-id="4212c-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Voce Restart All Affected](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="4212c-173">le voci del pulsante **Restart** possono essere diverse per altri servizi.</span><span class="sxs-lookup"><span data-stu-id="4212c-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="4212c-174">Dopo il riavvio dei servizi, usare il pulsante **Service Actions** per **Disattivare la modalità di manutenzione**.</span><span class="sxs-lookup"><span data-stu-id="4212c-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="4212c-175">Questa opzione indica ad Ambari di riprendere il monitoraggio per gli avvisi relativi al servizio.</span><span class="sxs-lookup"><span data-stu-id="4212c-175">This Ambari to resume monitoring for alerts for the service.</span></span>

