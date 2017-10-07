---
title: aaaUse Apache Storm con Power BI - HDInsight di Azure | Documenti Microsoft
description: Creare un report di Power BI con i dati da una topologia C# in esecuzione in un cluster Apache Storm in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Utilizzare i dati di Power BI toovisualize da una topologia di Apache Storm

Power BI consente toovisually visualizzare i dati dei report. Questo documento viene fornito un esempio di come toouse Apache Storm sui dati toogenerate HDInsight per Power BI.

> [!NOTE]
> Hello passaggi descritti in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio. progetto compilato Hello può essere cluster HDInsight basati su Linux tooa inviato. Solo i cluster basati su Linux creati dopo il 28/10/2016 supportano le topologie SCP.NET.
>
> toouse una topologia c# con un cluster basato su Linux, hello aggiornamento pacchetto Microsoft.SCP.Net.SDK NuGet usato dal tooversion progetto 0.10.0.6 o versione successiva. versione di Hello del pacchetto di hello deve corrispondere anche versione principale di hello di Storm installato in HDInsight. Ad esempio, le versioni 3.3 e 3.4 di Storm in HDInsight usano Storm versione 0.10.x, mentre HDInsight 3.5 usa Storm 1.0.x.
>
> C# topologie nei cluster basati su Linux è necessario utilizzare .NET 4.5 e toorun Mono nel cluster HDInsight hello. Anche se non dovrebbero verificarsi problemi, Tuttavia è necessario controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento per potenziali problemi di incompatibilità.
>
> Per una versione Java di questo progetto, che funziona con HDInsight basato su Linux o Windows, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Prerequisiti

* Un utente di Azure Active Directory con accesso [Power BI](https://powerbi.com).
* Un cluster HDInsight. Per altre informazioni, vedere [Introduzione a Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (una delle seguenti versioni di hello)

  * Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017, qualsiasi edizione

* Strumenti HDInsight per Visual Studio Hello: vedere [iniziare a usare gli strumenti di HDInsight hello per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) per informazioni sull'installazione delle informazioni.

## <a name="how-it-works"></a>Funzionamento

Questo esempio contiene una topologia Storm C# che genera in modo casuale i dati di log di Internet Information Services (IIS). Questi dati vengono quindi scritti tooa Database SQL, e da qui è usato toogenerate report in Power BI.

Hello file implementare hello funzionalità principale dell'esempio seguente:

* **SqlAzureBolt.cs**: scrive le informazioni prodotte in hello Storm topologia tooSQL Database.
* **IISLogsTable.sql**: hello Transact-SQL istruzioni utilizzate toogenerate hello database hello vengono memorizzati in.

> [!WARNING]
> Creare la tabella hello in Database SQL prima di avviare topologia hello il cluster HDInsight.

## <a name="download-hello-example"></a>Scaricare l'esempio hello

Scaricare hello [esempio HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, una divisione/clone utilizzando [git](http://git-scm.com/), oppure utilizzare hello **scaricare** toodownload collegamento zip dell'archivio di hello.

## <a name="create-a-database"></a>Creare un database

1. toocreate un database, utilizzare i passaggi di hello in hello [esercitazione Database SQL](../sql-database/sql-database-get-started.md) documento.

2. Connessione database toohello hello seguente passaggi hello [tooa Database SQL di connettersi con Visual Studio](../sql-database/sql-database-connect-query.md) documento.

3. In Esplora oggetti, fare doppio clic su database hello e selezionare **nuova Query**. Incolla il contenuto di hello di hello **IISLogsTable.sql** i file inclusi in hello scaricato progetto nella finestra query hello e quindi utilizzare Ctrl + Maiusc + query hello tooexecute di E. Verrà visualizzato un messaggio che hello comandi completati.

## <a name="configure-hello-sample"></a>Configurare l'esempio hello

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il database SQL. Da hello **Essentials** sezione di hello SQL pannello database, seleziona **Mostra le stringhe di connessione di database**. Elenco hello visualizzato, copiare hello **ADO.NET (autenticazione di SQL)** informazioni.

2. Aprire l'esempio hello in Visual Studio. Da **Esplora**aprire hello **app** file e quindi trovare hello seguente voce:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Sostituire hello **TOBEFILLED # # # #** valore con una stringa di connessione database hello copiato nel passaggio precedente hello. Sostituire **{la\_nome utente}** e **{la\_password}** con hello username e password per il database di hello.

3. Salvare e chiudere il file hello.

## <a name="deploy-hello-sample"></a>Distribuire l'esempio hello

1. Da **Esplora**, hello rapida **StormToSQL** del progetto e selezionare **inviare tooStorm in HDInsight**. Cluster HDInsight hello selezionare da hello **Cluster Storm** finestra di dialogo elenco a discesa.

   > [!NOTE]
   > Potrebbe richiedere alcuni secondi per hello **Cluster Storm** toopopulate elenco a discesa con i nomi dei server.
   >
   > Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure. Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.

2. Quando è stata inviata la topologia hello, hello __Visualizzatore della topologia__ viene visualizzato. tooview questa topologia, la voce SqlAzureWriterTopology hello selezionare dall'elenco di hello.

    ![topologie di Hello, con la topologia di hello selezionato](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    È possibile utilizzare questo toosee Visualizza informazioni sulla topologia di hello o fare doppio clic su un componente di tooa specifico ingresso (ad esempio hello SqlAzureBolt) toosee informazioni nella topologia hello.

3. Dopo hello topologia è stato eseguito per alcuni minuti, finestra di query SQL toohello restituito è stato utilizzato il database di hello toocreate. Sostituire le istruzioni di hello esistente con hello seguente query:

        select * from iislogs;

    Utilizzare Ctrl + MAIUSC + E tooexecute hello query e si deve ricevere toohello di risultati simile dati seguenti:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Questi dati sono state scritte dalla topologia Storm hello.

## <a name="create-a-report"></a>Creare un report

1. Connettersi toohello [connettore Database SQL di Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) per Power BI. 

2. In **Database** selezionare **Recupera**.

3. Selezionare **Database SQL di Azure** e quindi **Connetti**.

    > [!NOTE]
    > Potrebbe essere richiesto toodownload hello Power BI Desktop toocontinue. In questo caso, utilizzare hello tooconnect i passaggi seguenti:
    >
    > 1. Aprire Power BI Desktop e selezionare __Recupera dati__.
    > 2 Selezionare __Azure__ e quindi __Database SQL di Azure__.

4. Immettere hello informazioni tooconnect tooyour Database SQL di Azure. È possibile trovare queste informazioni visitando hello [portale di Azure](https://portal.azure.com) e selezionando il database SQL.

   > [!NOTE]
   > È inoltre possibile impostare l'intervallo di aggiornamento hello e filtri personalizzati utilizzando **abilitare opzioni avanzate** da hello finestra di dialogo di connessione.

5. Dopo aver stabilito la connessione, verrà visualizzato un nuovo set di dati con hello che stesso nome del database hello si è connessi. Selezionare hello dataset toobegin progettazione di un report.

6. Da **campi**, espandere hello **IISLOGS** voce. toocreate deriva un report che elenchi hello URI, selezionare la casella di controllo di hello per **URISTEM**.

    ![Creazione di un report](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Trascinare quindi **metodo** toohello report. deriva hello toolist gli aggiornamenti di Hello report e il metodo HTTP corrispondente di hello usata per hello richiesta HTTP.

    ![aggiunta di dati di hello (metodo)](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Da hello **visualizzazioni** colonna, seleziona hello **campi** icona e quindi selezionare hello freccia giù accanto troppo**metodo** in hello **valori**sezione. Selezionare toodisplay ha avuto un conteggio di quante volte un URI, **conteggio**.

    ![Modifica il numero di tooa dei metodi](./media/hdinsight-storm-power-bi-topology/count.png)

9. Selezionare quindi hello **istogramma in pila** toochange la modalità di visualizzazione di informazioni hello.

    ![Modifica grafico in pila di tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. report di hello toosave, selezionare **salvare** e immettere un nome per il report hello.

## <a name="stop-hello-topology"></a>Arrestare la topologia hello

topologia Hello continua toorun fino a quando non si arresta o Elimina hello Storm nel cluster HDInsight. toostop hello topologia, eseguire hello alla procedura seguente:

1. In Visual Studio, restituire toohello Visualizzatore della topologia e selezionare la topologia hello.

2. Seleziona hello **Kill** topologia di hello toostop pulsante.

    ![Kill pulsante sulla topologia di hello riepilogo](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Eliminare il cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passaggi successivi

In questo documento, si è appreso come toosend dati da un tooSQL topologia Storm Database, quindi visualizzare i dati di hello usando Power BI. Per informazioni su come toowork con altre tecnologie di Azure utilizzando Storm in HDInsight, vedere hello seguente documento:

* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)
