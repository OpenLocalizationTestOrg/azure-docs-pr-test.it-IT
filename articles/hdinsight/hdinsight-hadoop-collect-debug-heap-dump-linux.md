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
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dump dell'heap contengono uno snapshot di memoria dell'applicazione hello, inclusi i valori di hello delle variabili in fase di hello dump hello è stato creato. Si rivelano quindi utili per diagnosticare i problemi che si verificano in fase di esecuzione.

> [!IMPORTANT]
> Hello passaggi descritti in questo documento funzionano solo con i cluster HDInsight che utilizzano Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whichServices"></a>Services

È possibile abilitare dump dell'heap per hello seguenti servizi:

* **hcatalog** - tempelton
* **hive** - hiveserver2, metastore, derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager, nodemanager, timelineserver
* **hdfs** - datanode, secondarynamenode, namenode

È anche possibile abilitare i dump di heap per la mappa hello e ridurre i processi eseguiti da HDInsight.

## <a name="configuration"></a>Informazioni sulla configurazione dei dump dell'heap

Dump dell'heap sono abilitati per il passaggio di opzioni (talvolta nota anche come opts, o parametri) toohello JVM quando un servizio viene avviato. Per la maggior parte dei servizi Hadoop, è possibile modificare queste opzioni hello shell script utilizzato toostart hello servizio toopass.

In ogni script è presente un'esportazione per  **\* \_OPTS**, che contiene le opzioni di hello passato toohello JVM. Ad esempio, in hello **hadoop env.sh** riga hello che inizia con, script `export HADOOP_NAMENODE_OPTS=` contiene le opzioni di hello per hello NameNode servizio.

Eseguire il mapping e ridurre i processi sono leggermente diversi, perché queste operazioni sono un processo figlio di hello servizio MapReduce. Ogni mapping o ridurre il processo viene eseguito in un contenitore figlio e sono presenti due voci che contengono le opzioni di JVM hello. Entrambi sono contenuti in **mapred-site.xml**:

* **mapreduce.admin.map.child.java.opts**
* **mapreduce.admin.reduce.child.java.opts**

> [!NOTE]
> È consigliabile con Ambari toomodify entrambi hello script e le impostazioni di mapred-Site.XML, come Ambari gestiscono la replica delle modifiche tra i nodi cluster hello. Vedere hello [Ambari utilizzando](#using-ambari) sezione per i passaggi specifici.

### <a name="enable-heap-dumps"></a>Abilitare i dump dell'heap

Hello opzione seguente consente il dump di heap quando si verifica un OutOfMemoryError:

    -XX:+HeapDumpOnOutOfMemoryError

Hello  **+**  indica che questa opzione è abilitata. valore predefinito di Hello è disabled.

> [!WARNING]
> Dump dell'heap non sono abilitati per i servizi Hadoop in HDInsight per impostazione predefinita, come i file di dump hello possono essere di grandi dimensioni. Se li si abilita per la risoluzione dei problemi, tenere presente toodisable li dopo avere riprodotto hello problema e i file di dump hello raccolti.

### <a name="dump-location"></a>Percorso dei dump

Hello percorso predefinito file di dump hello è directory di lavoro corrente hello. È possibile controllare dove hello file verrà archiviati utilizzando hello seguente opzione:

    -XX:HeapDumpPath=/path

Ad esempio, usando `-XX:HeapDumpPath=/tmp` provoca hello dump toobe archiviato nella directory /tmp hello.

### <a name="scripts"></a>Script

È anche possibile generare uno script quando si verifica un **OutOfMemoryError** . Ad esempio, attivare una notifica per sapere di tale errore hello si è verificato. Seguente hello utilizzare opzione tootrigger uno script in un __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Poiché Hadoop è un sistema distribuito, qualsiasi script utilizzato deve essere inserito in tutti i nodi cluster hello eseguito sul servizio hello.
> 
> script Hello deve inoltre essere in una posizione accessibile da hello account hello viene eseguito il servizio come ed è necessario fornire le autorizzazioni di esecuzione. Ad esempio, è preferibile script toostore in `/usr/local/bin` e utilizzare `chmod go+rx /usr/local/bin/filename.sh` toogrant autorizzazioni read ed execute.

## <a name="using-ambari"></a>Uso di Ambari

configurazione di hello toomodify per un servizio, utilizzare hello alla procedura seguente:

1. Aprire hello Ambari web dell'interfaccia utente per il cluster. URL di Hello è https://YOURCLUSTERNAME.azurehdinsight.net.

    Quando richiesto, eseguire l'autenticazione del sito toohello utilizzando un nome di account hello HTTP (impostazione predefinita: amministratore) e la password per il cluster.

   > [!NOTE]
   > Potrebbero essere richieste una seconda volta da Ambari hello nome di utente e password. In questo caso, immettere hello stesso nome di account e password

2. Utilizzando l'elenco di hello di hello sinistra, selezionare l'area del servizio hello desiderato toomodify. Ad esempio, **HDFS**. Nell'area centrale hello selezionare hello **configurazioni** scheda.

    ![Immagine dell'interfaccia Web di Ambari con la scheda HDFS Configs selezionata](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Utilizzo di hello **filtro...**  voce, immettere **opts**. Vengono visualizzati solo gli elementi che contengono questo testo.

    ![Elenco filtrato](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Trovare hello  **\* \_OPTS** voce per il servizio di hello tooenable dump di heap per desiderato e aggiungere opzioni hello desidera tooenable. Nella seguente immagine di hello, ho aggiunto `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** voce:

    ![HADOOP_NAMENODE_OPTS con -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Quando abilitare i dump di heap per hello eseguire il mapping o ridurre il processo figlio, cercare i campi di hello denominati **mapreduce.admin.map.child.java.opts** e **mapreduce.admin.reduce.child.java.opts**.

    Hello utilizzare **salvare** pulsante modifiche hello toosave. È possibile immettere una breve nota che descrive le modifiche di hello.

5. Una volta hello modifiche sono state applicate, hello **richiesto riavvio** viene visualizzata l'icona accanto a uno o più servizi.

    ![icona restart required e pulsante restart](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Selezionare ogni servizio che richiede un riavvio e utilizzare hello **azioni servizio** pulsante troppo**attivare la modalità di manutenzione**. Modalità di manutenzione impedisce avvisi vengono generati dal servizio hello dopo il riavvio.

    ![Menu Turn on maintenance mode](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Dopo aver abilitato la modalità di manutenzione, utilizzare hello **riavviare** pulsante per il servizio hello troppo**riavviare effettuati tutti**

    ![Voce Restart All Affected](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > le voci per hello Hello **riavviare** pulsante può essere diverso per altri servizi.

8. Una volta hello servizi siano stati riavviati, utilizzare hello **azioni servizio** pulsante troppo**attivare la modalità manutenzione**. Questo tooresume Ambari monitoraggio per gli avvisi per il servizio di hello.

