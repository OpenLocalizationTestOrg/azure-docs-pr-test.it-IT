---
title: aaaTroubleshoot YARN tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Hadoop YARN e Azure HDInsight.
keywords: Azure HDInsight, YARN, domande frequenti, guida alla risoluzione dei problemi, domande comuni
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="1a2a2-104">Risolvere i problemi di YARN tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a2a2-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="1a2a2-105">Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload di Apache Hadoop YARN in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="1a2a2-106">Come creare una nuova coda YARN in un cluster</span><span class="sxs-lookup"><span data-stu-id="1a2a2-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="1a2a2-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="1a2a2-107">Resolution steps</span></span> 

<span data-ttu-id="1a2a2-108">Seguente hello utilizzare i passaggi in Ambari toocreate una nuova coda YARN e quindi bilanciare allocazione capacità hello tra tutte le code di hello.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="1a2a2-109">In questo esempio, due code esistente (**predefinito** e **thriftsvr**) sono cambiati da 50% della capacità too25% capacità, che offre hello nuova coda (spark) 50% della capacità.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="1a2a2-110">Coda</span><span class="sxs-lookup"><span data-stu-id="1a2a2-110">Queue</span></span> | <span data-ttu-id="1a2a2-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="1a2a2-111">Capacity</span></span> | <span data-ttu-id="1a2a2-112">Capacità massima</span><span class="sxs-lookup"><span data-stu-id="1a2a2-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a2a2-113">default</span><span class="sxs-lookup"><span data-stu-id="1a2a2-113">default</span></span> | <span data-ttu-id="1a2a2-114">25%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-114">25%</span></span> | <span data-ttu-id="1a2a2-115">50%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-115">50%</span></span> |
| <span data-ttu-id="1a2a2-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="1a2a2-116">thrftsvr</span></span> | <span data-ttu-id="1a2a2-117">25%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-117">25%</span></span> | <span data-ttu-id="1a2a2-118">50%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-118">50%</span></span> |
| <span data-ttu-id="1a2a2-119">Spark</span><span class="sxs-lookup"><span data-stu-id="1a2a2-119">spark</span></span> | <span data-ttu-id="1a2a2-120">50%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-120">50%</span></span> | <span data-ttu-id="1a2a2-121">50%</span><span class="sxs-lookup"><span data-stu-id="1a2a2-121">50%</span></span> |

1. <span data-ttu-id="1a2a2-122">Seleziona hello **Ambari viste** icona e il motivo di griglia hello quindi selezionare.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="1a2a2-123">Selezionare quindi **YARN Queue Manager** (Gestore code YARN).</span><span class="sxs-lookup"><span data-stu-id="1a2a2-123">Next, select **YARN Queue Manager**.</span></span>

    ![Selezionare l'icona delle visualizzazioni di Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="1a2a2-125">Seleziona hello **predefinito** coda.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-125">Select hello **default** queue.</span></span>

    ![Selezionare una coda predefinita dei messaggi hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="1a2a2-127">Per hello **predefinito** coda, modificare hello **capacità** da too25% 50%.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="1a2a2-128">Per hello **thriftsvr** coda, modificare hello **capacità** too25%.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Modificare % too25 capacità di hello per le code predefinite e thriftsvr hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="1a2a2-130">Selezionare una nuova coda, toocreate **aggiungere coda**.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Selezionare Aggiungi coda](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="1a2a2-132">Nuova coda hello nome.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-132">Name hello new queue.</span></span>

    ![Nome coda hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="1a2a2-134">Lasciare hello **capacità** valori al 50% e quindi seleziona hello **azioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Selezionare il pulsante di azioni hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="1a2a2-136">Selezionare **Save and Refresh Queues** (Salva e aggiorna code).</span><span class="sxs-lookup"><span data-stu-id="1a2a2-136">Select **Save and Refresh Queues**.</span></span>

    ![Selezionare Save and Refresh Queues (Salva e aggiorna code)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="1a2a2-138">Queste modifiche sono visibili immediatamente su hello dell'interfaccia utente dell'utilità di pianificazione di YARN.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="1a2a2-139">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1a2a2-139">Additional reading</span></span>

- [<span data-ttu-id="1a2a2-140">Utilità di pianificazione della capacità di YARN</span><span class="sxs-lookup"><span data-stu-id="1a2a2-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="1a2a2-141">Come scaricare i log di YARN da un cluster</span><span class="sxs-lookup"><span data-stu-id="1a2a2-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="1a2a2-142">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="1a2a2-142">Resolution steps</span></span> 

1. <span data-ttu-id="1a2a2-143">Connettere il cluster di HDInsight toohello tramite un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="1a2a2-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="1a2a2-144">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="1a2a2-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="1a2a2-145">toolist tutti hello ID applicazione di applicazioni YARN hello attualmente in esecuzione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="1a2a2-146">Hello sono elencati gli ID in hello **APPLICATIONID** colonna.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="1a2a2-147">È possibile scaricare i log da hello **APPLICATIONID** colonna.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-147">You can download logs from hello **APPLICATIONID** column.</span></span>

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. <span data-ttu-id="1a2a2-148">i registri di toodownload YARN contenitore per tutti gli schemi di applicazione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="1a2a2-149">Verrà creato un file di log denominato amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="1a2a2-150">i registri di contenitore YARN toodownload per solo hello più recente dell'applicazione master, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="1a2a2-151">Verrà creato un file di log denominato latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="1a2a2-152">i registri di contenitore YARN toodownload per hello prima applicazione due gli schemi, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="1a2a2-153">Verrà creato un file di log denominato first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="1a2a2-154">utilizzare tutti i log di contenitore YARN, toodownload hello il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="1a2a2-155">Verrà creato un file di log denominato logs.txt.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="1a2a2-156">toodownload hello YARN contenitore log per un contenitore specifico, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1a2a2-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="1a2a2-157">Verrà creato un file di log denominato containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="1a2a2-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="1a2a2-158"><a name="additional-reading-2"></a>Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1a2a2-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="1a2a2-159">Connettersi con SSH tooHDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="1a2a2-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="1a2a2-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Concetti e applicazioni di Apache Hadoop YARN)</span><span class="sxs-lookup"><span data-stu-id="1a2a2-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







