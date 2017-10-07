---
title: aaaJava-funzione definita dall'utente (UDF) con Hive in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toocreate basato su Java definito dall'utente (funzione) (funzione definita dall'utente) che funziona con Hive. Funzione definita dall'utente in questo esempio converte una tabella di toolowercase stringhe di testo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Utilizzare una UDF Java con Hive in HDInsight

Informazioni su come toocreate basato su Java definito dall'utente (funzione) (funzione definita dall'utente) che funziona con Hive. Hello Java funzione definita dall'utente in questo esempio converte una tabella di stringhe tooall minuscole dei caratteri del testo.

## <a name="requirements"></a>Requisiti

* Un cluster HDInsight 

    > [!IMPORTANT]
    > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    La maggior parte dei passaggi di questo documento vale per entrambi i cluster basati su Windows e Linux. Tuttavia, hello passaggi utilizzati tooupload hello compilata cluster toohello funzione definita dall'utente ed eseguire sono cluster basato su tooLinux specifici. Tooinformation che può essere utilizzato con i cluster basati su Windows vengono forniti collegamenti.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 o versione successiva (o equivalente, ad esempio OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* Un editor di testo o ambiente IDE Java

    > [!IMPORTANT]
    > Se si crea hello file Python in un client Windows, è necessario utilizzare un editor che utilizza LF come una terminazione di riga. Se non si è certi se l'editor utilizza LF o CRLF, vedere hello [Troubleshooting](#troubleshooting) sezione per i passaggi per la rimozione di hello carattere CR.

## <a name="create-an-example-java-udf"></a>Creare una UDF Java di esempio 

1. Dalla riga di comando, utilizzare hello toocreate un nuovo progetto di Maven seguenti:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Se si usa PowerShell, è necessario racchiuderlo tra virgolette i parametri di hello. ad esempio `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Questo comando crea una directory denominata **exampleudf**, che contiene progetti Maven hello.

2. Dopo aver creato il progetto di hello, eliminare hello **exampleudf/src/test** directory in cui è stato creato come parte del progetto hello.

3. Aprire hello **exampleudf/pom.xml**e sostituire hello `<dependencies>` voce con hello XML seguente:

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    Queste voci specifichino la versione di hello di Hadoop e Hive incluso in HDInsight 3.5. È possibile trovare informazioni sulle versioni di hello di Hadoop e Hive fornito con HDInsight da hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.

    Aggiungere un `<build>` sezione prima hello `</project>` riga alla fine di hello del file hello. In questa sezione deve contenere hello XML seguente:

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```

    Queste voci definiscono come toobuild hello progetto. In particolare, versione di hello Java che hello progetto usa e in che modo toobuild un uberjar per cluster toohello di distribuzione.

    Dopo che sono state apportate modifiche hello, salvare file hello.

4. Rinominare **exampleudf/src/main/java/com/microsoft/examples/App.java** troppo**ExampleUDF.java**e quindi aprire il file hello nell'editor.

5. Sostituire il contenuto di hello di hello **ExampleUDF.java** file con il seguente hello, quindi salvare il file hello.

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    Questo codice implementa una funzione definita dall'utente che accetta un valore di stringa e restituisce una versione a caratteri minuscola della stringa hello.

## <a name="build-and-install-hello-udf"></a>Compilare e installare hello funzione definita dall'utente

1. Utilizzare hello successivo comando toocompile e pacchetto hello funzione definita dall'utente:

    ```bash
    mvn compile package
    ```

    Questo comando Compila e pacchetti hello funzione definita dall'utente in hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.

2. Hello utilizzare `scp` del cluster di HDInsight toohello comando toocopy hello file.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Sostituire `myuser` con hello account utente SSH per il cluster. Sostituire `mycluster` con il nome del cluster hello. Se si utilizza un hello toosecure password SSH account, si è password hello tooenter richiesta. Se si utilizza un certificato, potrebbe essere necessario hello toouse `-i` parametro toospecify hello file di chiave privata.

3. Connettere il cluster toohello tramite SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

4. Dalla sessione SSH hello, copiare archiviazione tooHDInsight file jar di hello.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Utilizzare hello funzione definita dall'utente dall'Hive

1. Utilizzare i seguenti client di Beeline toostart hello dalla sessione SSH hello hello.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Questo comando si presuppone che sia stato utilizzato predefinito hello **admin** per account di accesso hello per il cluster.

2. Dopo aver concluso hello `jdbc:hive2://localhost:10001/>` richiesto, immettere hello seguente tooadd hello funzione definita dall'utente tooHive e che venga esposto come una funzione.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > Questo esempio si presuppone che l'archiviazione di Azure è archivio predefinito per il cluster hello. Se il cluster utilizza invece l'archivio Data Lake, modificare hello `wasb:///` valore troppo`adl:///`.

3. Utilizzare hello UDF tooconvert valori recuperati da una stringa di case toolower tabella.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    La query Seleziona hello piattaforma del dispositivo (Android, Windows, iOS, e così via) dalla tabella hello, convertire hello stringa toolower maiuscole e quindi visualizzarli. output di Hello viene visualizzato toohello simile, il testo seguente:

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a>Passaggi successivi

Per altri modi toowork con Hive, vedere [utilizzare Hive con HDInsight](hdinsight-use-hive.md).

Per ulteriori informazioni sulle funzioni Hive User-Defined, vedere [Hive operatori e funzioni definite dall'utente](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sezione wiki di Hive hello in apache.org.
