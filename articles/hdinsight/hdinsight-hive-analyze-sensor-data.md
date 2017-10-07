---
title: dati del sensore aaaAnalyze con Hive e Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati del sensore tooanalyze utilizzando hello la Console di Query Hive con HDInsight (Hadoop), quindi visualizzare i dati in Microsoft Excel con PowerView hello.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>Analizzare i dati del sensore utilizzando la Console di Query Hive hello in Hadoop in HDInsight

Informazioni su come dati del sensore tooanalyze utilizzando hello la Console di Query Hive con HDInsight (Hadoop), quindi visualizzare i dati di hello in Microsoft Excel tramite Power View.

> [!IMPORTANT]
> Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


In questo esempio, utilizzare i dati cronologici tooprocess Hive e identificare i problemi con i sistemi di riscaldamento e aria condizionata. In particolare, identificare i sistemi sono tooreliably non è possibile mantenere una temperatura set eseguendo hello seguenti attività:

* Creare tabelle di HIVE tooquery dati archiviati in file separati da virgole (CSV) file.
* Creare query HIVE dati hello tooanalyze.
* i dati analizzato hello tooretrieve, utilizzare tooHDInsight tooconnect Microsoft Excel.
* dati hello toovisualize, utilizzare Power View.

![Un diagramma dell'architettura della soluzione hello](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>Prerequisiti

* Cluster HDInsight (Hadoop) - Per informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel viene usato per la visualizzazione dei dati con [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).

* [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>esempio hello toorun

1. Dal web browser, passare toohello URL seguente: 

         https://<clustername>.azurehdinsight.net

    Sostituire `<clustername>` con nome hello del cluster HDInsight.

    Quando richiesto, eseguire l'autenticazione tramite nome utente dell'amministratore hello e la password utilizzati durante il provisioning di questo cluster.

2. Dalla pagina web hello visualizzata, fare clic su hello **raccolta di introduzione** scheda, quindi in hello **soluzioni con dati di esempio** categoria, fare clic su hello **analisi dei dati del sensore** esempio di.

    ![Immagine della raccolta introduttiva](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Istruzioni di hello fornita nell'esempio di hello toofinish hello pagina web.
