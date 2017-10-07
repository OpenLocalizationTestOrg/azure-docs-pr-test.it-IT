---
title: aaaCustomize Hadoop cluster per processo di analisi scientifica dei dati di Team hello | Documenti Microsoft
description: "Moduli di Python più diffusi resi disponibili nei cluster personalizzati Hadoop di Azure HDInsight."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Personalizzare i cluster di Azure HDInsight Hadoop per hello processo di analisi scientifica dei dati di Team
In questo articolo viene descritto come toocustomize un HDInsight Hadoop cluster tramite l'installazione a 64 bit Anaconda (Python 2.7) in ogni nodo quando viene eseguito il provisioning di cluster hello come un servizio HDInsight. Viene inoltre illustrato come tooaccess hello cluster toohello di nodo head toosubmit processi personalizzati. Questa personalizzazione rende molti moduli Python più diffusi, inclusi in Anaconda, funzioni definite (UDF) che sono facilmente disponibili per l'utilizzo in utente progettato tooprocess record Hive nel cluster hello. Per istruzioni sulle procedure hello utilizzate in questo scenario, vedere [come query Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

i menu seguenti Hello collega tootopics che descrivono come tooset backup hello diversi ambienti di analisi scientifica dei dati utilizzata dal hello [Team Data Science processo (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Personalizzare i cluster Hadoop di Azure HDInsight
avviare toocreate un cluster HDInsight Hadoop personalizzato, effettuando l'accesso troppo[**portale di Azure classico**](https://manage.windowsazure.com/), fare clic su **New** nell'angolo inferiore, hello a sinistra e quindi selezionare i servizi dati -> HDINSIGHT -> **creazione personalizzata** toobring backup hello **i dettagli del Cluster** finestra. 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Immettere il nome di hello di hello cluster toobe creato nella pagina configurazione 1 e accettare i valori predefiniti per hello altri campi. Fare clic su hello freccia toogo toohello pagina Configurazione successiva. 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Nella pagina configurazione 2, immettere il numero di hello di **nodi dati**selezionare hello **area/rete virtuale**e selezionare le dimensioni di hello di hello **nodo HEAD** e hello **Nodo dati**. Fare clic su hello freccia toogo toohello pagina Configurazione successiva.

> [!NOTE]
> Hello **area/rete virtuale** ha toobe hello stesso come area hello hello dell'account di archiviazione che verrà utilizzato per il cluster HDInsight Hadoop hello toobe. In caso contrario, nella pagina di configurazione quarto hello, account di archiviazione hello non apparirà nell'elenco a discesa hello di **nome ACCOUNT**.
> 
> 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Nella pagina Configurazione 3, fornire un nome utente e una password per hello cluster HDInsight Hadoop. **Non** hello seleziona *hello immettere Metastore Hive/Oozie*. Quindi, fare clic su hello freccia toogo toohello pagina Configurazione successiva. 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Nella pagina configurazione 4, specificare il nome di account di archiviazione hello, il contenitore predefinito hello di hello cluster HDInsight Hadoop. Se si seleziona *crea contenitore predefinito* in hello **contenitore predefinito** elenco a discesa, un contenitore con hello stesso nome, verrà creato il cluster hello. Fare clic su hello freccia toogo toohello ultima pagina di configurazione.

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

In hello finale **azioni Script** pagina di configurazione, fare clic su **aggiungere script azione** pulsante e compilare i campi di testo hello con i seguenti valori hello.

* **NOME** -qualsiasi stringa come nome hello di questa azione di script
* **TIPO DI NODO**: selezionare **Tutti i nodi**
* **URI SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* è un contenitore pubblico nell'account di archiviazione hello 
  * *getgoing* utilizziamo tooshare PowerShell script file toofacilitate il lavoro degli utenti in Azure
* **PARAMETRI**: lasciare vuoto

Infine, fare clic su hello segno di spunta toostart hello la creazione di cluster HDInsight Hadoop hello personalizzato. 

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Accedere hello nodo Head del Hadoop Cluster
Prima di poter accedere nodo head di hello del cluster Hadoop hello tramite RDP, è necessario abilitare cluster Hadoop toohello di accesso remoto in Azure. 

1. Accedi toohello [ **portale di Azure classico**](https://manage.windowsazure.com/)selezionare **HDInsight** hello sinistra, selezionare il cluster Hadoop hello elenco di cluster, fare clic su hello  **CONFIGURAZIONE** scheda e quindi fare clic su hello **ABILITA modalità remota** icona hello parte inferiore della pagina hello.
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. In hello **configurare Desktop remoto** finestra immettere hello nome utente e i campi PASSWORD e selezionare la data di scadenza hello per l'accesso remoto. Quindi fare clic su hello segno di spunta tooenable hello accesso remoto toohello nodo head del cluster Hadoop hello.
   
    ![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> nome utente Hello e una password per l'accesso remoto hello non sono il nome di utente hello e la password utilizzati durante la creazione di un cluster Hadoop hello. Si tratta di un set separato di credenziali. Data di scadenza hello di accesso remoto hello è inoltre toobe entro 7 giorni da hello data corrente.
> 
> 

Dopo aver abilitato l'accesso remoto, fare clic su **CONNETTI** nella parte inferiore di hello di hello pagina tooremote nel nodo head hello. Toohello nodo head del cluster Hadoop hello si accede tramite l'immissione di credenziali hello per utente di accesso remoto hello specificato in precedenza.

![Creare un'area di lavoro](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Hello passaggi successivi hello avanzate processo analitica vengono eseguito il mapping in hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere passaggi spostare i dati in HDInsight, quindi l'elaborazione e di esempio, in preparazione per l'apprendimento dai dati hello con Azure Machine Learning.

Vedere [come query Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) per istruzioni su come tooaccess hello moduli Python inclusi in Anaconda dal nodo head di hello del cluster di hello nelle funzioni definite dall'utente (UDF) che vengono utilizzati tooprocess Hive record archiviati cluster hello.

