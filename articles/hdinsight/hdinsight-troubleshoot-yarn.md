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
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Risolvere i problemi di YARN tramite Azure HDInsight

Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload di Apache Hadoop YARN in Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Come creare una nuova coda YARN in un cluster


### <a name="resolution-steps"></a>Procedura per la risoluzione 

Seguente hello utilizzare i passaggi in Ambari toocreate una nuova coda YARN e quindi bilanciare allocazione capacità hello tra tutte le code di hello. 

In questo esempio, due code esistente (**predefinito** e **thriftsvr**) sono cambiati da 50% della capacità too25% capacità, che offre hello nuova coda (spark) 50% della capacità.
| Coda | Capacity | Capacità massima |
| --- | --- | --- | --- |
| default | 25% | 50% |
| thrftsvr | 25% | 50% |
| Spark | 50% | 50% |

1. Seleziona hello **Ambari viste** icona e il motivo di griglia hello quindi selezionare. Selezionare quindi **YARN Queue Manager** (Gestore code YARN).

    ![Selezionare l'icona delle visualizzazioni di Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Seleziona hello **predefinito** coda.

    ![Selezionare una coda predefinita dei messaggi hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Per hello **predefinito** coda, modificare hello **capacità** da too25% 50%. Per hello **thriftsvr** coda, modificare hello **capacità** too25%.

    ![Modificare % too25 capacità di hello per le code predefinite e thriftsvr hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. Selezionare una nuova coda, toocreate **aggiungere coda**.

    ![Selezionare Aggiungi coda](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Nuova coda hello nome.

    ![Nome coda hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Lasciare hello **capacità** valori al 50% e quindi seleziona hello **azioni** pulsante.

    ![Selezionare il pulsante di azioni hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Selezionare **Save and Refresh Queues** (Salva e aggiorna code).

    ![Selezionare Save and Refresh Queues (Salva e aggiorna code)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Queste modifiche sono visibili immediatamente su hello dell'interfaccia utente dell'utilità di pianificazione di YARN.

### <a name="additional-reading"></a>Informazioni aggiuntive

- [Utilità di pianificazione della capacità di YARN](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Come scaricare i log di YARN da un cluster


### <a name="resolution-steps"></a>Procedura per la risoluzione 

1. Connettere il cluster di HDInsight toohello tramite un client Secure Shell (SSH). Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-2).

2. toolist tutti hello ID applicazione di applicazioni YARN hello attualmente in esecuzione, eseguire hello comando seguente:

    ```apache
    yarn top
    ```
    Hello sono elencati gli ID in hello **APPLICATIONID** colonna. È possibile scaricare i log da hello **APPLICATIONID** colonna.

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

3. i registri di toodownload YARN contenitore per tutti gli schemi di applicazione, utilizzare hello comando seguente:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Verrà creato un file di log denominato amlogs.txt. 

4. i registri di contenitore YARN toodownload per solo hello più recente dell'applicazione master, utilizzare hello comando seguente:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Verrà creato un file di log denominato latestamlogs.txt. 

4. i registri di contenitore YARN toodownload per hello prima applicazione due gli schemi, utilizzare hello comando seguente:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Verrà creato un file di log denominato first2amlogs.txt. 

5. utilizzare tutti i log di contenitore YARN, toodownload hello il seguente comando:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Verrà creato un file di log denominato logs.txt. 

6. toodownload hello YARN contenitore log per un contenitore specifico, utilizzare hello comando seguente:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Verrà creato un file di log denominato containerlogs.txt.

### <a name="additional-reading-2"></a>Informazioni aggiuntive

- [Connettersi con SSH tooHDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Concetti e applicazioni di Apache Hadoop YARN)







