---
title: aaaConnect tooHadoop di Excel con hello Hive Driver ODBC - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come tooset backup e utilizzare hello Hive driver ODBC Microsoft per i dati di Excel tooquery nel cluster HDInsight da Microsoft Excel.
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Connettere Excel tooHadoop in Azure HDInsight con hello Hive di Microsoft ODBC driver

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Soluzione Big Data Microsoft integra i componenti di Microsoft Business Intelligence (BI) con i cluster Apache Hadoop che sono stati distribuiti da hello Azure HDInsight. Un esempio di tale integrazione è hello possibilità tooconnect Excel toohello Hive del data warehouse di un cluster Hadoop in HDInsight mediante hello Driver Microsoft Hive Open Database Connectivity (ODBC).

È inoltre possibile tooconnect dati di hello associati a un cluster HDInsight e altre origini dati, inclusi altri (non-HDInsight) Hadoop cluster, da Excel utilizzando hello componente aggiuntivo di Microsoft Power Query per Excel. Per informazioni sull'installazione e utilizzo di Power Query, vedere [tooHDInsight Excel connettersi con Power Query][hdinsight-power-query].

> [!NOTE]
> Mentre hello i passaggi questo articolo può essere utilizzato con uno Linux o cluster HDInsight basati su Windows, Windows è richiesto per workstation client hello.
> 
> 

**Prerequisiti**:

Prima di iniziare questo articolo, è necessario disporre di hello seguenti elementi:

* **Un cluster HDInsight**. toocreate uno, vedere [Guida introduttiva di Azure HDInsight][hdinsight-get-started].
* **Una workstation** con Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.

## <a name="install-microsoft-hive-odbc-driver"></a>Installare Microsoft Hive ODBC driver
Scaricare e installare il Driver Microsoft ODBC Hive dal hello [area Download][hive-odbc-driver-download].

Questo driver può essere installato nelle versioni a 32 bit o 64 bit di Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012. driver Hello consente tooAzure connessione HDInsight (versione 1.6 e versioni successive) e l'emulatore di Azure HDInsight (v.1.0.0.0 e versioni successive). Installare versione hello corrispondente versione di hello di un'applicazione hello in cui si usa il driver ODBC hello. Per questa esercitazione, il driver hello viene utilizzato da Office Excel.

## <a name="create-hive-odbc-data-source"></a>Creare un'origine dati Hive ODBC
Hello passaggi seguenti viene illustrato come toocreate un Hive origine dati ODBC.

1. In Windows 8 o Windows 10, premere la schermata iniziale hello Windows tooopen chiave hello e quindi digitare **origini dati**.
2. Fare clic su **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** a seconda della versione di Office. Se si usa Windows 7, scegliere **Configura origini dati ODBC (32 bit)** o **Configura origini dati ODBC (64 bit)** da **Strumenti di amministrazione**. Verrà visualizzato hello **Amministrazione origine dati ODBC** finestra di dialogo.
   
    ![Amministrazione origine dati ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurare un DSN usando l'amministrazione origine dati ODBC")

3. Da utente DNS, fare clic su **Aggiungi** tooopen hello **Crea nuova origine dati** procedura guidata.
4. Selezionare **Microsoft Hive ODBC Driver** e quindi fare clic su **Fine**. Verrà visualizzato hello **Hive ODBC Driver DNS installazione di Microsoft** finestra di dialogo.
5. Digitare o selezionare hello seguenti valori:
   
   | Proprietà | Descrizione |
   | --- | --- |
   |  Data Source Name |Fornire un'origine dati di nome tooyour |
   |  Host |Immettere &lt;HDInsightClusterName>.azurehdinsight.net. Ad esempio, myHDICluster.azurehdinsight.net |
   |  Porta |Utilizzare <strong>443</strong>. (Questa porta è stata modificata da too443 563). |
   |  Database |Usare l'<strong>impostazione predefinita</strong>. |
   |  Mechanism |Selezionare <strong>Azure HDInsight Service</strong> |
   |  User Name |Immettere il nome utente HTTP del cluster HDInsight. nome utente predefinito Hello <strong>admin</strong>. |
   |  Password |Immettere la password utente del cluster HDInsight. |
   
    </table>
   
    Esistono alcuni toobe importanti parametri conoscere quando fa clic su **opzioni avanzate**:
   
   | . | Descrizione |
   | --- | --- |
   |  Use Native Query |Quando è selezionata, il driver ODBC di hello non tenta tooconvert TSQL in HiveQL. Deve essere usato solo se si è assolutamente certi di inviare istruzioni HiveQL pure. Quando ci si connette tooSQL Server o Database SQL di Azure, è necessario lasciarla deselezionata. |
   |  Rows fetched per block |Durante il recupero di un numero elevato di record, l'ottimizzazione di questo parametro può essere prestazioni ottimali tooensure obbligatorio. |
   |  Default string column length, Binary column length, Decimal column scale |lunghezza del tipo di dati Hello e precisione possono influire sulle modalità di restituzione di dati. Provocano toobe informazioni non corrette restituite scadenza tooloss di precisione e/o il troncamento. |

    ![Opzioni avanzate](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opzioni di configurazione DSN avanzate")

1. Fare clic su **Test** origine dati di tootest hello. Quando l'origine dati hello è configurata correttamente, viene visualizzato *verifica completata!*.
2. Fare clic su **OK** finestra di dialogo tooclose hello Test. nuova origine dei dati Hello è elencati in hello **Amministrazione origine dati ODBC**.
3. Fare clic su **OK** guidata hello tooexit.

## <a name="import-data-into-excel-from-hdinsight"></a>Importazione di dati in Excel da HDInsight
Hello passaggi seguenti descrivono hello modo tooimport dati da una tabella Hive in una cartella di lavoro di Excel utilizzando l'origine di dati ODBC hello creato nella sezione precedente hello.

1. Aprire una cartella di lavoro nuova o esistente in Excel.
2. Da hello **dati** scheda, fare clic su **recupera dati**, fare clic su **da altre origini**, quindi fare clic su **da ODBC** toolaunch hello  **Connessione guidata dati**.
   
    ![Aprire la Connessione guidata dati](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Aprire la Connessione guidata dati")
4. Nome creato nell'ultima sezione hello dell'origine dati selezionare hello e quindi scegliere **OK**.
5. Immettere nome utente di Hadoop (nome predefinito hello è admin) hello password e quindi fare clic su **Connetti**.
6. Nello strumento di spostamento espandere **HIVE** e **default** e quindi fare clic su **hivesampletable** e infine su **Carica**. Alcuni secondi prima del recupero dei dati importati tooExcel necessario.

    ![Strumento di spostamento per Hive ODBC in HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Aprire Connessione guidata dati")


## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato descritto come toouse hello dati tooretrieve del driver ODBC di Microsoft Hive da hello HDInsight Service in Excel. Analogamente, è possibile recuperare dati da hello HDInsight Service nel Database SQL. È inoltre dati tooupload possibili in un HDInsight Service. toolearn informazioni, vedere:

* [Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-data]
* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


