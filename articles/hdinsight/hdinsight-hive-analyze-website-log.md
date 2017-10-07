---
title: aaaUse Hive con Hadoop per l'analisi dei log del sito Web - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su modalità di registrazione toouse Hive con sito Web tooanalyze HDInsight. Verranno utilizzare un file di log come input in una tabella di HDInsight e utilizzare i dati di hello tooquery HiveQL."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a>Usare l'Hive con i log di tooanalyze HDInsight basati su Windows dai siti Web
Informazioni su modalità di registrazione toouse HiveQL con tooanalyze HDInsight da un sito Web. Analisi dei log del sito Web può essere utilizzato toosegment i destinatari in base alle attività simili, classificare i visitatori del sito da dati demografici e toofind visualizzano il contenuto di hello, provengono da siti Web di hello e così via.

> [!IMPORTANT]
> Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

In questo esempio, si utilizzerà una HDInsight cluster tooanalyze sito Web log file tooget approfondite frequenza hello del sito Web di toohello visite a siti Web esterni in un giorno. Verrà anche generato un riepilogo degli errori di sito Web che gli utenti di hello. Si apprenderà come:

* Connettersi tooa archiviazione Blob di Azure, che contiene i file di registro del sito Web.
* Creare HIVE tabelle tooquery tali log.
* Creare query HIVE dati hello tooanalyze.
* Utilizzare Microsoft Excel tooconnect tooHDInsight (utilizzando i dati di hello analizzato tooretrieve di open database connectivity (ODBC).

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a>Prerequisiti
* È necessario avere completato il provisioning di un cluster Hadoop in Azure HDInsight. Per istruzioni, vedere [Provisioning di cluster HDInsight][hdinsight-provision].
* È necessario aver installato Microsoft Excel 2013 o Excel 2010.
* È necessario disporre di [Driver ODBC di Microsoft Hive](http://www.microsoft.com/download/details.aspx?id=40886) dati tooimport dall'Hive in Excel.

## <a name="toorun-hello-sample"></a>esempio hello toorun
1. Da hello [portale Azure](https://portal.azure.com/), dalla schermata iniziale (se è stato aggiunto sono cluster hello) hello, fare clic su riquadro cluster hello in cui si desidera toorun: esempio hello.
2. Da hello cluster pannello in **collegamenti rapidi**, fare clic su **Dashboard Cluster**e quindi da hello **Dashboard del Cluster** pannello, fare clic su **HDInsight Cluster Dashboard**. In alternativa, è possibile aprire direttamente il dashboard di hello utilizzando hello URL seguente:

         https://<clustername>.azurehdinsight.net

    Quando richiesto, eseguire l'autenticazione tramite nome utente dell'amministratore hello e la password utilizzati durante il provisioning di cluster hello.
3. Dalla pagina web hello visualizzata, fare clic su hello **raccolta di introduzione** scheda, quindi in hello **soluzioni con dati di esempio** categoria, fare clic su hello **analisi dei Log del sito Web** esempio di.
4. Istruzioni di hello fornita nell'esempio di hello toofinish hello pagina web.

## <a name="next-steps"></a>Passaggi successivi
Provare hello seguente esempio: [analisi dei dati del sensore con Hive di HDInsight](hdinsight-hive-analyze-sensor-data.md).

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
