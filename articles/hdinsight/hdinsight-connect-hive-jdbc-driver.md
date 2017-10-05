---
title: Eseguire una query Hive tramite il driver JDBC - Azure HDInsight | Microsoft Docs
description: Usare il driver JDBC da un'applicazione Java per inviare query Hive a Hadoop in HDInsight. Connettersi a livello di codice e dal client SQuirrel SQL.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: f2de58c2763b2ddd0926336164738929c477c4ae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="e8bca-104">Eseguire una query Hive tramite il driver JDBC in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="e8bca-105">Informazioni su come usare il driver JDBC da un'applicazione Java per inviare query Hive a Hadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="e8bca-106">Questo documento illustra come eseguire la connessione a livello di programmazione e dal client SQuirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="e8bca-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="e8bca-107">Per altre informazioni sull'interfaccia Hive JDBC, vedere [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="e8bca-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8bca-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e8bca-108">Prerequisites</span></span>

* <span data-ttu-id="e8bca-109">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="e8bca-110">Sono adatti i cluster basati su Linux o su Windows.</span><span class="sxs-lookup"><span data-stu-id="e8bca-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e8bca-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e8bca-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e8bca-112">Per altre informazioni, vedere [Ritiro di HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e8bca-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e8bca-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="e8bca-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="e8bca-114">SQuirreL è un'applicazione client JDBC.</span><span class="sxs-lookup"><span data-stu-id="e8bca-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="e8bca-115">[Java Developer Kit (JDK) versione 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o successiva.</span><span class="sxs-lookup"><span data-stu-id="e8bca-115">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="e8bca-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="e8bca-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="e8bca-117">Maven è un sistema di compilazione per progetti Java, usato dal progetto associato a questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e8bca-117">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="e8bca-118">Stringa di connessione JDBC</span><span class="sxs-lookup"><span data-stu-id="e8bca-118">JDBC connection string</span></span>

<span data-ttu-id="e8bca-119">Le connessioni JDBC a un cluster HDInsight in Azure vengono stabilite tramite la porta 443 e il traffico viene protetto usando SSL.</span><span class="sxs-lookup"><span data-stu-id="e8bca-119">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="e8bca-120">Il gateway pubblico dietro cui si trovano i cluster reindirizza il traffico alla porta su cui HiveServer2 è attualmente in ascolto.</span><span class="sxs-lookup"><span data-stu-id="e8bca-120">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="e8bca-121">Di seguito è riportato una stringa di connessione di esempio:</span><span class="sxs-lookup"><span data-stu-id="e8bca-121">The following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="e8bca-122">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-122">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="e8bca-123">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e8bca-123">Authentication</span></span>

<span data-ttu-id="e8bca-124">Quando si stabilisce la connessione, è necessario usare il nome amministratore e la password del cluster HDInsight per l'autenticazione nel gateway cluster.</span><span class="sxs-lookup"><span data-stu-id="e8bca-124">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="e8bca-125">Durante la connessione dai client JDBC come SQuirreL SQL, è necessario immettere il nome amministratore e la password nelle impostazioni del client.</span><span class="sxs-lookup"><span data-stu-id="e8bca-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="e8bca-126">Da un'applicazione Java è necessario usare il nome e la password quando viene stabilita una connessione.</span><span class="sxs-lookup"><span data-stu-id="e8bca-126">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="e8bca-127">Ad esempio, il codice Java seguente apre una nuova connessione usando la stringa di connessione, il nome amministratore e la password:</span><span class="sxs-lookup"><span data-stu-id="e8bca-127">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="e8bca-128">Connettersi con il client SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="e8bca-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="e8bca-129">SQuirreL SQL è un client JDBC che può essere usato per eseguire in modalità remota query Hive con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-129">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="e8bca-130">I passaggi seguenti presuppongono che sia già stato installato SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="e8bca-130">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="e8bca-131">Copiare i driver JDBC Hive dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-131">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="e8bca-132">Per **HDInsight basato su Linux**, seguire questa procedura per scaricare i file JAR necessari.</span><span class="sxs-lookup"><span data-stu-id="e8bca-132">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="e8bca-133">Creare la directory che contiene i file.</span><span class="sxs-lookup"><span data-stu-id="e8bca-133">Create a directory that contains the files.</span></span> <span data-ttu-id="e8bca-134">Ad esempio, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="e8bca-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="e8bca-135">Dalla riga di comando usare i comandi seguenti per copiare i file dal cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e8bca-135">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="e8bca-136">Sostituire `USERNAME` con il nome dell'account utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="e8bca-136">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="e8bca-137">Sostituire `CLUSTERNAME` con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-137">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

    * <span data-ttu-id="e8bca-138">Per **HDInsight basato su Windows**, seguire questa procedura per scaricare i file JAR.</span><span class="sxs-lookup"><span data-stu-id="e8bca-138">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="e8bca-139">Nel portale di Azure selezionare il cluster HDInsight e quindi selezionare l'icona **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="e8bca-139">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![Icona Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="e8bca-141">Nel pannello Desktop remoto fare clic sul pulsante **Connetti** per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="e8bca-141">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="e8bca-142">Se Desktop remoto non è abilitato, usare il modulo per specificare un nome utente e una password, quindi selezionare **Abilita** per abilitare Desktop remoto per il cluster.</span><span class="sxs-lookup"><span data-stu-id="e8bca-142">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![Pannello Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="e8bca-144">Dopo avere selezionato **Connetti** verrà scaricato un file con estensione rdp.</span><span class="sxs-lookup"><span data-stu-id="e8bca-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="e8bca-145">Usare questo file per avviare il client Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="e8bca-145">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="e8bca-146">Quando richiesto, usare il nome utente e la password immessi per Accesso desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="e8bca-146">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="e8bca-147">Una volta stabilita la connessione, copiare i file seguenti dalla sessione Desktop remoto nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e8bca-147">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="e8bca-148">Inserirli in una directory locale denominata `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="e8bca-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="e8bca-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="e8bca-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="e8bca-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="e8bca-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="e8bca-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="e8bca-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="e8bca-152">I numeri di versione inclusi nei percorsi e i nomi file potrebbero essere diversi per il cluster in uso.</span><span class="sxs-lookup"><span data-stu-id="e8bca-152">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="e8bca-153">Disconnettere la sessione di Desktop remoto al termine della copia dei file.</span><span class="sxs-lookup"><span data-stu-id="e8bca-153">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="e8bca-154">Avviare l'applicazione SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="e8bca-154">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="e8bca-155">Nella parte sinistra della finestra selezionare **Drivers** (Driver).</span><span class="sxs-lookup"><span data-stu-id="e8bca-155">From the left of the window, select **Drivers**.</span></span>

    ![Scheda Drivers sul lato sinistro della finestra](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="e8bca-157">Nella parte superiore della finestra di dialogo **Drivers** (Driver) selezionare l'icona **+** per creare un driver.</span><span class="sxs-lookup"><span data-stu-id="e8bca-157">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![Icone Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="e8bca-159">Nella finestra di dialogo di aggiunta del driver aggiungere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8bca-159">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="e8bca-160">**Name** (Nome): Hive</span><span class="sxs-lookup"><span data-stu-id="e8bca-160">**Name**: Hive</span></span>
    * <span data-ttu-id="e8bca-161">**Example URL** (URL di esempio): `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="e8bca-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="e8bca-162">**Extra Class Path** (Percorso classe extra): usare il pulsante Add (Aggiungi) per aggiungere i file JAR scaricati in precedenza</span><span class="sxs-lookup"><span data-stu-id="e8bca-162">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="e8bca-163">**Class Name** (Nome classe): org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="e8bca-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![finestra di dialogo add driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="e8bca-165">Fare clic su **OK** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="e8bca-165">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="e8bca-166">Nella parte sinistra della finestra di SQL SQuirreL selezionare **Aliases** (Alias).</span><span class="sxs-lookup"><span data-stu-id="e8bca-166">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="e8bca-167">Fare quindi clic sull'icona **+** per creare un alias di connessione.</span><span class="sxs-lookup"><span data-stu-id="e8bca-167">Then click the **+** icon to create a connection alias.</span></span>

    ![aggiungere un nuovo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="e8bca-169">Usare i valori seguenti per la finestra di dialogo **Add Alias** (Aggiungi alias).</span><span class="sxs-lookup"><span data-stu-id="e8bca-169">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="e8bca-170">**Name** (Nome): Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="e8bca-171">**Driver**: usare l'elenco a discesa per selezionare il driver **Hive**</span><span class="sxs-lookup"><span data-stu-id="e8bca-171">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="e8bca-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="e8bca-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="e8bca-173">Sostituire **CLUSTERNAME** con il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-173">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="e8bca-174">**User Name** (Nome utente): nome dell'account di accesso per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-174">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="e8bca-175">Il valore predefinito è `admin`.</span><span class="sxs-lookup"><span data-stu-id="e8bca-175">The default is `admin`.</span></span>

    * <span data-ttu-id="e8bca-176">**Password**: password per l'account di accesso del cluster.</span><span class="sxs-lookup"><span data-stu-id="e8bca-176">**Password**: The password for the cluster login account.</span></span>

 ![finestra di dialogo add alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="e8bca-178">Usare il pulsante **Test** per verificare il funzionamento della connessione.</span><span class="sxs-lookup"><span data-stu-id="e8bca-178">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="e8bca-179">Quando viene visualizzata la finestra di dialogo **Connect to: Hive on HDInsight** (Connetti a: Hive in HDInsight), selezionare **Connect** (Connetti) per eseguire il test.</span><span class="sxs-lookup"><span data-stu-id="e8bca-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="e8bca-180">Se il test ha esito positivo, verrà visualizzata la finestra di dialogo **Connection successful** (Connessione riuscita).</span><span class="sxs-lookup"><span data-stu-id="e8bca-180">If the test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="e8bca-181">Usare il pulsante **OK** nella parte inferiore della finestra di dialogo **Add Alias** (Aggiungi alias) per salvare l'alias di connessione.</span><span class="sxs-lookup"><span data-stu-id="e8bca-181">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

7. <span data-ttu-id="e8bca-182">Nell'elenco a discesa **Connect to** (Connetti a) nella parte superiore di SQL SQuirreL selezionare **Hive on HDInsight** (Hive in HDInsight).</span><span class="sxs-lookup"><span data-stu-id="e8bca-182">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="e8bca-183">Quando richiesto, selezionare **Connect** (Connetti).</span><span class="sxs-lookup"><span data-stu-id="e8bca-183">When prompted, select **Connect**.</span></span>

    ![finestra di dialogo di connessione](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="e8bca-185">Dopo avere stabilito la connessione, immettere la query seguente nella finestra di dialogo di query SQL e quindi selezionare l'icona **Run** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="e8bca-185">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="e8bca-186">Nell'area dei risultati dovrebbero comparire i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="e8bca-186">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![finestra della query sql, con i risultati](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="e8bca-188">Connettersi da un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="e8bca-188">Connect from an example Java application</span></span>

<span data-ttu-id="e8bca-189">Un esempio dell'uso di un client Java per eseguire una query Hive in HDInsight è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="e8bca-189">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="e8bca-190">Seguire le istruzioni del repository per compilare ed eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e8bca-190">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e8bca-191">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e8bca-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="e8bca-192">Errore imprevisto durante il tentativo di aprire una connessione SQL</span><span class="sxs-lookup"><span data-stu-id="e8bca-192">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="e8bca-193">**Sintomi**: quando ci si connette a un cluster HDInsight versione 3.3 o 3.4, un errore potrebbe segnalare che si è verificato un errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="e8bca-193">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="e8bca-194">L'analisi dello stack dell'errore inizia con le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8bca-194">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="e8bca-195">**Causa**: questo errore è causato da una mancata corrispondenza tra la versione del file commons-codec.jar usato da SQuirreL e la versione necessaria per i componenti Hive JDBC.</span><span class="sxs-lookup"><span data-stu-id="e8bca-195">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components.</span></span>

<span data-ttu-id="e8bca-196">**Soluzione**: per risolvere l'errore eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e8bca-196">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="e8bca-197">Scaricare il file commons-codec.jar dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-197">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="e8bca-198">Uscire da SQuirreL e passare alla directory in cui è installato SQuirreL nel sistema.</span><span class="sxs-lookup"><span data-stu-id="e8bca-198">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="e8bca-199">Nella directory `lib` della directory di SquirreL sostituire il file commons-codec.jar esistente con quello scaricato dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-199">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="e8bca-200">Riavviare SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="e8bca-200">Restart SQuirreL.</span></span> <span data-ttu-id="e8bca-201">L'errore non dovrebbe più verificarsi quando ci si connette a Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-201">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8bca-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8bca-202">Next steps</span></span>

<span data-ttu-id="e8bca-203">Dopo avere appreso come usare JDBC con Hive, vedere i collegamenti seguenti per scoprire altre modalità di utilizzo di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8bca-203">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="e8bca-204">Caricare dati in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-204">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="e8bca-205">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e8bca-206">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e8bca-207">Usare processi MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8bca-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
