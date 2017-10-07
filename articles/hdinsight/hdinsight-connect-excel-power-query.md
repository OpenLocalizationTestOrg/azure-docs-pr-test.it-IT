---
title: aaaConnect tooHadoop di Excel con Power Query - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come sfruttare tootake componenti di business intelligence e usare Power Query per i dati di Excel tooaccess archiviati in Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Connettere Excel tooHadoop tramite Power Query
Una caratteristica fondamentale di una soluzione big data di Microsoft hello è integrazione hello dei componenti di Microsoft business intelligence (BI) con i cluster Hadoop in HDInsight di Azure. Un esempio principale è hello possibilità tooconnect Excel toohello account di archiviazione di Azure che contiene dati hello associati al cluster Hadoop usando hello Microsoft Power Query per il componente aggiuntivo di Excel. In questo articolo illustra come gestire la tooset backup e utilizzare dati tooquery Power Query associati a un cluster Hadoop con HDInsight.

### <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:

* **Un cluster HDInsight**. tooconfigure uno, vedere [Guida introduttiva di Azure HDInsight][hdinsight-get-started].
* **Una workstation** che esegue il sistema operativo Windows 7, Windows Server 2008 R2 o una versione successiva.
* **Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 Standalone oppure Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Installare Power Query
Power Query consente di importare dati derivati o generati da un processo Hadoop in esecuzione su un cluster HDInsight.

In Excel 2016, Power Query è stata integrata sulla barra multifunzione dati di hello in Get hello & sezione Transform. Per le versioni precedenti di Excel, scaricare Microsoft Power Query per Excel da hello [Microsoft Download Center] [ powerquery-download] e installarlo.

## <a name="import-hdinsight-data-into-excel"></a>Importare dati di HDInsight in Excel
Hello il componente aggiuntivo Power Query per Excel rende facile tooimport dati dal cluster HDInsight in Excel, in strumenti di Business Intelligence, ad esempio PowerPivot e Power mappa possono essere tooinspect usato, analizzare e presentare dati hello.

**tooimport dati da un cluster di HDInsight**

1. Aprire Excel.
2. Creare una nuova cartella di lavoro vuota.
3. Eseguire hello basato sulla versione di Excel hello come segue:

    - Excel 2016

        - Fare clic su hello **dati** menu, fare clic su **recupera dati** da hello **recupera e trasforma** della barra multifunzione, fare clic su **da Azure**, quindi fare clic su  **Da Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Fare clic su hello **Power Query** menu, fare clic su **da Azure**, quindi fare clic su **da Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Nota:** se non viene visualizzato hello **Power Query** dal menu Vai troppo**File** > **opzioni** > **Add-Ins**e selezionare **componenti aggiuntivi COM** dall'elenco a discesa hello **Gestisci** casella nella parte inferiore di hello della pagina hello. Seleziona hello **Vai...**  pulsante e verificare che la casella di hello per hello Power Query per il componente aggiuntivo di Excel è stato eseguito.
       
        **Nota:** Power Query consente inoltre dati tooimport da HDFS facendo **da altre origini**.
4. Per **nome Account**, immettere il nome di hello dell'account di archiviazione Blob di Azure hello associato al cluster e quindi fare clic su **OK**. Questo account può essere hello [account di archiviazione predefinito](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) o un account di archiviazione collegato.  formato hello è *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Per **chiave dell'Account**, immetterne hello per hello account di archiviazione Blob e quindi fare clic su **salvare**. (È necessaria hello solo informazioni tooenter hello account prima che accedere a questo archivio).
6. In hello **Navigator** hello riquadro a sinistra dell'Editor di Query hello fare doppio clic sul nome del contenitore di archiviazione Blob di hello. Per impostazione predefinita, il nome di contenitore hello è hello stesso nome come nome del cluster hello.
7. Individuare **HiveSampleData.txt** in hello **nome** colonna (percorso della cartella hello **... / hive/warehouse hivesampletable/**), quindi fare clic su **binario** a sinistra di hello di HiveSampleData.txt. HiveSampleData.txt include tutti i cluster di hello. Facoltativamente, è possibile usare un proprio file.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Se si desidera, è possibile rinominare i nomi di colonna hello. Quando si è pronti, fare clic sul pulsante **Chiudi e carica**.  dati Hello sono stato caricato tooyour cartella di lavoro:
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso toouse dati Power Query tooretrieve HDInsight in Excel. È analogamente possibile recuperare dati da HDInsight nel database SQL di Azure. È inoltre dati possibili tooupload in HDInsight. toolearn informazioni, vedere hello seguenti articoli:

* [Connettere Excel tooHDInsight con il Driver ODBC di Hive Microsoft hello][hdinsight-ODBC]
* [Caricare dati tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
