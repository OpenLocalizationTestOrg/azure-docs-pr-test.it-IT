---
title: aaaUse c# con Hive e Pig in Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse c# definito dall'utente (UDF) di funzioni con Hive e Pig streaming in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>Usare le funzioni definite dall'utente C# con lo streaming Hive e Pig in Hadoop in HDInsight

Informazioni su come toouse c# funzioni definite dall'utente (UDF) con Apache Hive e Pig in HDInsight.

> [!IMPORTANT]
> passaggi di Hello in questo documento di lavoro con i cluster HDInsight basati su Linux sia basato su Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'articolo sul [controllo delle versioni del componente di HDInsight](hdinsight-component-versioning.md).

Entrambi Hive e Pig passare applicazioni tooexternal dati per l'elaborazione. Questo processo è noto come _streaming_. Quando si utilizza un'applicazione .NET, i dati di hello vengono trasferiti toohello applicazione STDIN e un'applicazione hello restituisce i risultati di hello in STDOUT. tooread e scrittura da STDIN e STDOUT, è possibile utilizzare `Console.ReadLine()` e `Console.WriteLine()` da un'applicazione console.

## <a name="prerequisites"></a>Prerequisiti

* Una familiarità nello scrivere e nel compilare il codice C# destinato a .NET Framework 4.5.

    * Usare qualsiasi IDE desiderato. Si consigliano [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 o [Visual Studio Code](https://code.visualstudio.com/). Hello passaggi di questo utilizzo di documento, Visual Studio 2017.

* Un .exe tooupload modo file toohello cluster ed esecuzione di processi Pig e Hive. È consigliabile hello Data Lake Tools per Visual Studio, Azure PowerShell e CLI di Azure. Hello passaggi descritti in questo documento utilizzano gli strumenti di hello Data Lake per i file di Visual Studio tooupload hello ed eseguire query Hive di esempio hello.

    Per informazioni su altre query Hive toorun di modi e processi Pig, vedere hello seguenti documenti:

    * [Usare Apache Hive con HDInsight](hdinsight-use-hive.md)

    * [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

* Un cluster Hadoop in HDInsight. Per altre informazioni sulla creazione di un cluster, vedere [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET su HDInsight

* __HDInsight basati su Linux__ cluster tramite [Mono (https://mono-project.com)](https://mono-project.com) toorun le applicazioni .NET. La versione Mono 4.2.1 è inclusa nella versione 3.5 di HDInsight.

    Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse una versione specifica di Mono, vedere hello [installazione o aggiornamento Mono](hdinsight-hadoop-install-mono.md) documento.

* __HDInsight basati su Windows__ cluster utilizzino le applicazioni .NET di hello Microsoft .NET CLR toorun.

Per ulteriori informazioni sulla versione di hello di hello .NET framework e Mono inclusa con le versioni di HDInsight, vedere [versioni dei componenti di HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Creare hello C\# progetti

### <a name="hive-udf"></a>UDF di Hive

1. Aprire Visual Studio e creare una soluzione. Tipo di progetto hello selezionare **applicazione Console (.NET Framework)**e nome hello nuovo progetto **HiveCSharp**.

    > [!IMPORTANT]
    > Selezionare __.NET Framework 4.5__ se si usa un cluster HDInsight basato su Linux. Per altre informazioni sulla compatibilità Mono con le versioni di .NET Framework, vedere il documento relativo alla [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Sostituire il contenuto di hello di **Program.cs** con seguenti hello:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Compilare il progetto hello.

### <a name="pig-udf"></a>UDF di Pig

1. Aprire Visual Studio e creare una soluzione. Tipo di progetto hello selezionare **applicazione Console**e nome hello nuovo progetto **PigUDF**.

2. Sostituire il contenuto di hello di hello **Program.cs** file con hello seguente codice:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Questa applicazione analizza linee hello inviate da Pig e riformatta righe che iniziano con `java.lang.Exception`.

3. Salvare **Program.cs**e quindi compilare il progetto hello.

## <a name="upload-toostorage"></a>Caricare toostorage

1. In Visual Studio aprire **Esplora server**.

2. Espandere **Azure** e quindi **HDInsight**.

3. Se richiesto, immettere le credenziali della sottoscrizione di Azure, quindi fare clic su **Accedi**.

4. Espandere i cluster HDInsight hello che si desidera toodeploy per questa applicazione. Una voce con il testo hello __(Account di archiviazione predefinito)__ è elencato.

    ![Esplora server con l'account di archiviazione hello per cluster hello](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Se questa voce può essere espanso, si utilizza un __Account di archiviazione Azure__ come spazio di archiviazione predefinito per il cluster hello. tooview hello i file di archiviazione predefiniti hello per cluster hello, espandere la voce hello e quindi fare doppio clic su hello __(contenitore predefinito)__.

    * Se non è possibile espandere questa voce, si utilizza __archivio Azure Data Lake__ come spazio di archiviazione predefinito hello per cluster hello. file di hello tooview in spazio di archiviazione predefinito hello for cluster hello, fare doppio clic su hello __(Account di archiviazione predefinito)__ voce.

6. file di .exe tooupload hello, utilizzare uno dei seguenti metodi hello:

    * Se si utilizza un __Account di archiviazione Azure__, fare clic sull'icona di caricamento hello e quindi selezionare toohello **bin\debug** cartella per hello **HiveCSharp** progetto. Infine, selezionare hello **HiveCSharp.exe** file e fare clic su **Ok**.

        ![icona relativa al caricamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Se si utilizza __archivio Azure Data Lake__, fare doppio clic su un'area vuota nell'elenco di file hello e quindi selezionare __caricare__. Infine, selezionare hello **HiveCSharp.exe** file e fare clic su **aprire**.

    Una volta hello __HiveCSharp.exe__ ha completato il caricamento, il processo di caricamento hello ripetizione per hello __PigUDF.exe__ file.

## <a name="run-a-hive-query"></a>Eseguire una query Hive

1. In Visual Studio aprire **Esplora server**.

2. Espandere **Azure** e quindi **HDInsight**.

3. Cluster hello pulsante destro del mouse che è stato distribuito hello **HiveCSharp** applicazione e quindi selezionare **scrivere una Query Hive**.

4. Utilizzare hello seguente testo per query Hive hello:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Rimuovere il commento hello `add file` istruzione corrispondente tipo hello spazio di archiviazione predefinito utilizzato per il cluster.

    Questa query Seleziona hello `clientid`, `devicemake`, e `devicemodel` i campi dal `hivesampletable`e passa i campi di hello toohello HiveCSharp.exe applicazione. query Hello prevede hello tooreturn tre campi dell'applicazione, che vengono archiviati come `clientid`, `phoneLabel`, e `phoneHash`. query Hello prevede inoltre toofind HiveCSharp.exe nella radice di hello del contenitore di archiviazione predefinito hello.

5. Fare clic su **Invia** il cluster HDInsight toohello di toosubmit hello processo. Hello **riepilogo Hive** verrà visualizzata la finestra.

6. Fare clic su **aggiornare** toorefresh hello riepilogo finché **lo stato del processo** cambia troppo**completato**. il processo di hello tooview output, fare clic su **Output processo**.

## <a name="run-a-pig-job"></a>Eseguire un processo Pig

1. Utilizzare uno dei seguenti cluster HDInsight di metodi tooconnect tooyour hello:

    * Se si usa un cluster HDInsight __basato su Linux__, usare SSH. Ad esempio, `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Per altre informazioni, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Se si utilizza un __basati su Windows__ cluster HDInsight, [cluster toohello Connetti tramite Desktop remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Utilizzare una hello riga di comando toostart hello Pig comando seguente:

        pig

    > [!IMPORTANT]
    > Se si utilizza un cluster basato su Windows, utilizzare hello seguente invece di comandi:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    Viene visualizzato un prompt `grunt>`.

3. Immettere hello seguente toorun un processo Pig che utilizza un'applicazione hello .NET Framework:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Hello `DEFINE` istruzione crea un alias di `streamer` Applications pigudf.exe hello e `CACHE` caricamento dei dati dall'archivio predefinito per il cluster hello. In un secondo momento, `streamer` viene utilizzato con hello `STREAM` tooprocess operatore hello singole righe contenute nel LOG e dati hello restituito come una serie di colonne.

    > [!NOTE]
    > nome dell'applicazione Hello è utilizzato per il flusso deve essere racchiuso tra hello \` (apice inverso) carattere quando alias, e ' (virgoletta singola) utilizzato con `SHIP`.

4. Dopo aver immesso l'ultima riga hello, deve iniziare il processo di hello. Restituisce toohello simili di output il testo seguente:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Passaggi successivi

In questo documento, si è appreso come toouse un'applicazione .NET Framework dall'Hive e Pig in HDInsight. Se si desidera vedere toouse Python con Hive e Pig, toolearn [usare Python con Hive e Pig in HDInsight](hdinsight-python.md).

Per altri modi toouse Pig e Hive e toolearn sull'utilizzo di MapReduce, vedere hello seguenti documenti:

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)
