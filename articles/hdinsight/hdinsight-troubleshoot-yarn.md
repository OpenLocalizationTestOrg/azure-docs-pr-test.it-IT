---
title: Risolvere i problemi di YARN tramite Azure HDInsight | Microsoft Docs
description: Risposte alle domande frequenti sull'utilizzo di Apache Hadoop YARN e Azure HDInsight.
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
ms.openlocfilehash: 63f2d88ad59661b7fbcffd0aaeb94c58d40bdb73
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="47f72-104">Risolvere i problemi di YARN tramite Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="47f72-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="47f72-105">Informazioni sui problemi principali che possono verificarsi quando si usano i payload di Apache Hadoop YARN in Apache Ambari unitamente alle risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="47f72-105">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="47f72-106">Come creare una nuova coda YARN in un cluster</span><span class="sxs-lookup"><span data-stu-id="47f72-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="47f72-107">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="47f72-107">Resolution steps</span></span> 

<span data-ttu-id="47f72-108">Seguire questa procedura in Ambari per creare una nuova coda YARN e bilanciare l'allocazione delle capacità tra tutte le code.</span><span class="sxs-lookup"><span data-stu-id="47f72-108">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span></span> 

<span data-ttu-id="47f72-109">In questo esempio è stata modificata la capacità dal 50% al 25% per due code esistenti (**predefinita** e **thriftsvr**), in modo da consentire alla nuova coda (Spark) di avere una capacità del 50%.</span><span class="sxs-lookup"><span data-stu-id="47f72-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="47f72-110">Coda</span><span class="sxs-lookup"><span data-stu-id="47f72-110">Queue</span></span> | <span data-ttu-id="47f72-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="47f72-111">Capacity</span></span> | <span data-ttu-id="47f72-112">Capacità massima</span><span class="sxs-lookup"><span data-stu-id="47f72-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47f72-113">default</span><span class="sxs-lookup"><span data-stu-id="47f72-113">default</span></span> | <span data-ttu-id="47f72-114">25%</span><span class="sxs-lookup"><span data-stu-id="47f72-114">25%</span></span> | <span data-ttu-id="47f72-115">50%</span><span class="sxs-lookup"><span data-stu-id="47f72-115">50%</span></span> |
| <span data-ttu-id="47f72-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="47f72-116">thrftsvr</span></span> | <span data-ttu-id="47f72-117">25%</span><span class="sxs-lookup"><span data-stu-id="47f72-117">25%</span></span> | <span data-ttu-id="47f72-118">50%</span><span class="sxs-lookup"><span data-stu-id="47f72-118">50%</span></span> |
| <span data-ttu-id="47f72-119">Spark</span><span class="sxs-lookup"><span data-stu-id="47f72-119">spark</span></span> | <span data-ttu-id="47f72-120">50%</span><span class="sxs-lookup"><span data-stu-id="47f72-120">50%</span></span> | <span data-ttu-id="47f72-121">50%</span><span class="sxs-lookup"><span data-stu-id="47f72-121">50%</span></span> |

1. <span data-ttu-id="47f72-122">Selezionare l'icona **Visualizzazioni di Ambari** e scegliere il motivo di griglia.</span><span class="sxs-lookup"><span data-stu-id="47f72-122">Select the **Ambari Views** icon, and then select the grid pattern.</span></span> <span data-ttu-id="47f72-123">Selezionare quindi **YARN Queue Manager** (Gestore code YARN).</span><span class="sxs-lookup"><span data-stu-id="47f72-123">Next, select **YARN Queue Manager**.</span></span>

    ![Selezionare l'icona Visualizzazioni di Ambari](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="47f72-125">Selezionare la coda **predefinita**.</span><span class="sxs-lookup"><span data-stu-id="47f72-125">Select the **default** queue.</span></span>

    ![Selezionare la coda predefinita](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="47f72-127">Per la coda **predefinita**, modificare la **capacità** dal 50% al 25%.</span><span class="sxs-lookup"><span data-stu-id="47f72-127">For the **default** queue, change the **capacity** from 50% to 25%.</span></span> <span data-ttu-id="47f72-128">Per la coda **thriftsvr**, impostare la **capacità** sul 25%.</span><span class="sxs-lookup"><span data-stu-id="47f72-128">For the **thriftsvr** queue, change the **capacity** to 25%.</span></span>

    ![Impostare la capacità sul 25% per la coda predefinita e la coda thriftsvr](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="47f72-130">Per creare una nuova coda, fare clic su **Aggiungi coda**.</span><span class="sxs-lookup"><span data-stu-id="47f72-130">To create a new queue, select **Add Queue**.</span></span>

    ![Selezionare Aggiungi coda](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="47f72-132">Assegnare un nome alla nuova coda.</span><span class="sxs-lookup"><span data-stu-id="47f72-132">Name the new queue.</span></span>

    ![Assegnare alla coda il nome Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="47f72-134">Lasciare i valori di **Capacità** al 50% e selezionare il pulsante **Azioni**.</span><span class="sxs-lookup"><span data-stu-id="47f72-134">Leave the **capacity** values at 50%, and then select the **Actions** button.</span></span>

    ![Selezionare il pulsante Azioni](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="47f72-136">Selezionare **Save and Refresh Queues** (Salva e aggiorna code).</span><span class="sxs-lookup"><span data-stu-id="47f72-136">Select **Save and Refresh Queues**.</span></span>

    ![Selezionare Save and Refresh Queues (Salva e aggiorna code)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="47f72-138">Queste modifiche saranno immediatamente visibili nell'interfaccia utente dell'utilità di pianificazione YARN.</span><span class="sxs-lookup"><span data-stu-id="47f72-138">These changes are visible immediately on the YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="47f72-139">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47f72-139">Additional reading</span></span>

- [<span data-ttu-id="47f72-140">Utilità di pianificazione della capacità di YARN</span><span class="sxs-lookup"><span data-stu-id="47f72-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="47f72-141">Come scaricare i log di YARN da un cluster</span><span class="sxs-lookup"><span data-stu-id="47f72-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="47f72-142">Procedura per la risoluzione</span><span class="sxs-lookup"><span data-stu-id="47f72-142">Resolution steps</span></span> 

1. <span data-ttu-id="47f72-143">Connettersi al cluster HDInsight con un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="47f72-143">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="47f72-144">Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="47f72-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="47f72-145">Elencare tutti gli ID applicazione delle applicazioni YARN attualmente in esecuzione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-145">To list all the application IDs of the YARN applications that are currently running, run the following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="47f72-146">Gli ID sono elencati nella colonna **APPLICATIONID**,</span><span class="sxs-lookup"><span data-stu-id="47f72-146">The IDs are listed in the **APPLICATIONID** column.</span></span> <span data-ttu-id="47f72-147">di cui è necessario scaricare i log **APPLICATIONID**.</span><span class="sxs-lookup"><span data-stu-id="47f72-147">You can download logs from the **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="47f72-148">Per scaricare i log dei contenitori YARN per tutti gli schemi dell'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-148">To download YARN container logs for all application masters, use the following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="47f72-149">Verrà creato un file di log denominato amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="47f72-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="47f72-150">Per scaricare i log dei contenitori YARN solo per gli schemi dell'applicazione più recenti, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-150">To download YARN container logs for only the latest application master, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="47f72-151">Verrà creato un file di log denominato latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="47f72-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="47f72-152">Per scaricare i log dei contenitori YARN per i primi due schemi dell'applicazione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-152">To download YARN container logs for the first two application masters, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="47f72-153">Verrà creato un file di log denominato first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="47f72-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="47f72-154">Per scaricare tutti i log dei contenitori YARN, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-154">To download all YARN container logs, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="47f72-155">Verrà creato un file di log denominato logs.txt.</span><span class="sxs-lookup"><span data-stu-id="47f72-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="47f72-156">Per scaricare il log dei contenitori YARN per un determinato contenitore, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="47f72-156">To download the YARN container log for a specific container, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="47f72-157">Verrà creato un file di log denominato containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="47f72-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="47f72-158"><a name="additional-reading-2"></a>Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="47f72-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="47f72-159">Connettersi a HDInsight (Hadoop) con SSH</span><span class="sxs-lookup"><span data-stu-id="47f72-159">Connect to HDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="47f72-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Concetti e applicazioni di Apache Hadoop YARN)</span><span class="sxs-lookup"><span data-stu-id="47f72-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







