---
title: aaaQuery Hive tramite driver JDBC hello - HDInsight di Azure | Documenti Microsoft
description: Utilizzare il driver JDBC hello da una query tooHadoop di Java applicazione toosubmit Hive in HDInsight. Connettersi a livello di codice e dal client di SQL esce hello.
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
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="38f4c-104">Eseguire una query Hive tramite il driver JDBC hello in HDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="38f4c-105">Informazioni su come driver JDBC di hello toouse da un toosubmit applicazione Java Hive query tooHadoop in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="38f4c-106">informazioni di Hello in questo documento viene illustrato come tooconnect a livello di codice e da hello esce SQL client.</span><span class="sxs-lookup"><span data-stu-id="38f4c-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="38f4c-107">Per ulteriori informazioni su hello Hive interfaccia JDBC, vedere [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="38f4c-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f4c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="38f4c-108">Prerequisites</span></span>

* <span data-ttu-id="38f4c-109">Un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="38f4c-110">Sono adatti i cluster basati su Linux o su Windows.</span><span class="sxs-lookup"><span data-stu-id="38f4c-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="38f4c-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="38f4c-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="38f4c-112">Per altre informazioni, vedere [Ritiro di HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="38f4c-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="38f4c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="38f4c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="38f4c-114">SQuirreL è un'applicazione client JDBC.</span><span class="sxs-lookup"><span data-stu-id="38f4c-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="38f4c-115">Hello [Java Developer Kit (JDK) versione 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="38f4c-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="38f4c-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="38f4c-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="38f4c-117">Maven è un progetto di compilare il sistema per i progetti di linguaggio che viene utilizzato dal progetto hello associata a questo articolo.</span><span class="sxs-lookup"><span data-stu-id="38f4c-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="38f4c-118">Stringa di connessione JDBC</span><span class="sxs-lookup"><span data-stu-id="38f4c-118">JDBC connection string</span></span>

<span data-ttu-id="38f4c-119">Cluster di HDInsight tooan connessioni JDBC in Azure vengono eseguite su 443, e il traffico di hello viene protetto mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="38f4c-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="38f4c-120">gateway pubblica Hello cluster hello protette da reindirizza la porta toohello di traffico hello HiveServer2 è effettivamente in ascolto.</span><span class="sxs-lookup"><span data-stu-id="38f4c-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="38f4c-121">di seguito Hello è una stringa di connessione di esempio:</span><span class="sxs-lookup"><span data-stu-id="38f4c-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="38f4c-122">Sostituire `CLUSTERNAME` con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="38f4c-123">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="38f4c-123">Authentication</span></span>

<span data-ttu-id="38f4c-124">Quando si stabilisce la connessione hello, è necessario utilizzare hello HDInsight cluster admin nome e la password tooauthenticate toohello cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="38f4c-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="38f4c-125">Durante la connessione dal client JDBC, ad esempio esce SQL, è necessario immettere il nome di amministratore hello e una password nelle impostazioni client.</span><span class="sxs-lookup"><span data-stu-id="38f4c-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="38f4c-126">Da un'applicazione Java, è necessario utilizzare nome hello e una password per stabilire una connessione.</span><span class="sxs-lookup"><span data-stu-id="38f4c-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="38f4c-127">Ad esempio, hello codice Java seguente apre una nuova connessione utilizzando la stringa di connessione hello Nome amministratore e la password:</span><span class="sxs-lookup"><span data-stu-id="38f4c-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="38f4c-128">Connettersi con il client SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="38f4c-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="38f4c-129">Esce SQL è un client JDBC che può essere utilizzati tooremotely eseguire Hive query con il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="38f4c-130">Hello passaggi seguenti presuppongono che è già stato installato SQL esce.</span><span class="sxs-lookup"><span data-stu-id="38f4c-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="38f4c-131">Copiare i driver JDBC Hive hello dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="38f4c-132">Per **HDInsight basati su Linux**, utilizzare hello seguenti passaggi viene file jar di toodownload hello necessario.</span><span class="sxs-lookup"><span data-stu-id="38f4c-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="38f4c-133">Creare una directory che contiene file hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="38f4c-134">ad esempio `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="38f4c-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="38f4c-135">Dalla riga di comando, seguito hello utilizzare comandi file hello toocopy dal cluster HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="38f4c-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="38f4c-136">Sostituire `USERNAME` con nome dell'account utente SSH hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="38f4c-137">Sostituire `CLUSTERNAME` con nome del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="38f4c-138">Per **HDInsight basati su Windows**, i file jar di hello toodownload i passaggi seguenti di hello di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="38f4c-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="38f4c-139">Dal portale di Azure hello, selezionare il cluster HDInsight, quindi hello **Desktop remoto** icona.</span><span class="sxs-lookup"><span data-stu-id="38f4c-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Icona Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="38f4c-141">Nel Pannello di hello Desktop remoto, utilizzare hello **Connetti** cluster toohello tooconnect di pulsante.</span><span class="sxs-lookup"><span data-stu-id="38f4c-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="38f4c-142">Se non è abilitato hello Desktop remoto, usare hello modulo tooprovide un nome utente e password, quindi selezionare **abilitare** tooenable Desktop remoto per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Pannello Desktop remoto](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="38f4c-144">Dopo avere selezionato **Connetti** verrà scaricato un file con estensione rdp.</span><span class="sxs-lookup"><span data-stu-id="38f4c-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="38f4c-145">Utilizzare il client Desktop remoto hello toolaunch questo file.</span><span class="sxs-lookup"><span data-stu-id="38f4c-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="38f4c-146">Quando richiesto, utilizzare il nome di utente hello e la password che immessa per l'accesso Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="38f4c-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="38f4c-147">Una volta connessi, copiare i seguenti file dal computer locale tooyour sessione Desktop remoto hello hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="38f4c-148">Inserirli in una directory locale denominata `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="38f4c-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="38f4c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="38f4c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="38f4c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="38f4c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="38f4c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="38f4c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="38f4c-152">versione di Hello numeri inclusi in hello percorsi e nomi file potrebbero essere diversi per il cluster.</span><span class="sxs-lookup"><span data-stu-id="38f4c-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="38f4c-153">Disconnettere la sessione di Desktop remoto hello dopo aver completato la copia dei file hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="38f4c-154">Avviare un'applicazione hello esce SQL.</span><span class="sxs-lookup"><span data-stu-id="38f4c-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="38f4c-155">Da sinistra hello hello finestra, selezionare **driver**.</span><span class="sxs-lookup"><span data-stu-id="38f4c-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Scheda driver hello a sinistra della finestra hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="38f4c-157">Dalle icone hello nella parte superiore di hello di hello **driver** finestra di dialogo, seleziona hello  **+**  toocreate icona un driver.</span><span class="sxs-lookup"><span data-stu-id="38f4c-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Icone Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="38f4c-159">Nella finestra di dialogo Aggiungi Driver hello aggiungere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="38f4c-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="38f4c-160">**Name** (Nome): Hive</span><span class="sxs-lookup"><span data-stu-id="38f4c-160">**Name**: Hive</span></span>
    * <span data-ttu-id="38f4c-161">**Example URL** (URL di esempio): `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="38f4c-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="38f4c-162">**Percorso di classe aggiuntivo**: file jar utilizzare hello Aggiungi pulsante tooadd hello scaricato in precedenza</span><span class="sxs-lookup"><span data-stu-id="38f4c-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="38f4c-163">**Class Name** (Nome classe): org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="38f4c-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![finestra di dialogo add driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="38f4c-165">Fare clic su **OK** toosave queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="38f4c-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="38f4c-166">A sinistra hello della finestra SQL esce hello, selezionare **alias**.</span><span class="sxs-lookup"><span data-stu-id="38f4c-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="38f4c-167">Quindi fare clic su hello  **+**  toocreate icona un alias di connessione.</span><span class="sxs-lookup"><span data-stu-id="38f4c-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![aggiungere un nuovo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="38f4c-169">I valori seguenti di hello di utilizzo per hello **aggiungere Alias** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="38f4c-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="38f4c-170">**Name** (Nome): Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="38f4c-171">**Driver**: hello tooselect elenco a discesa di utilizzare hello **Hive** driver</span><span class="sxs-lookup"><span data-stu-id="38f4c-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="38f4c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="38f4c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="38f4c-173">Sostituire **CLUSTERNAME** con nome hello del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="38f4c-174">**Nome utente**: nome di account di accesso hello cluster per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="38f4c-175">valore predefinito di Hello è `admin`.</span><span class="sxs-lookup"><span data-stu-id="38f4c-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="38f4c-176">**Password**: password hello per account di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-176">**Password**: hello password for hello cluster login account.</span></span>

 ![finestra di dialogo add alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="38f4c-178">Hello utilizzare **Test** tooverify pulsante che hello connessione funzioni.</span><span class="sxs-lookup"><span data-stu-id="38f4c-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="38f4c-179">Quando **connettersi: Hive in HDInsight** viene visualizzata la finestra, selezionare **Connetti** test hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="38f4c-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="38f4c-180">Se il test di hello ha esito positivo, viene visualizzato un **connessione riuscita** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="38f4c-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="38f4c-181">connessione hello toosave utilizzare alias, hello **Ok** pulsante nella parte inferiore di hello di hello **aggiungere Alias** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="38f4c-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="38f4c-182">Da hello **connettersi** elenco a discesa in cima a hello esce SQL, selezionare **Hive in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="38f4c-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="38f4c-183">Quando richiesto, selezionare **Connect** (Connetti).</span><span class="sxs-lookup"><span data-stu-id="38f4c-183">When prompted, select **Connect**.</span></span>

    ![finestra di dialogo di connessione](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="38f4c-185">Una volta connessi, immettere hello eseguire una query nella finestra di dialogo query SQL hello seguenti e quindi selezionare hello **eseguire** icona.</span><span class="sxs-lookup"><span data-stu-id="38f4c-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="38f4c-186">area risultati Hello deve visualizzare i risultati di hello di hello query.</span><span class="sxs-lookup"><span data-stu-id="38f4c-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![finestra della query sql, con i risultati](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="38f4c-188">Connettersi da un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="38f4c-188">Connect from an example Java application</span></span>

<span data-ttu-id="38f4c-189">Un esempio di utilizzo di un tooquery client Java Hive in HDInsight è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="38f4c-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="38f4c-190">Seguire le istruzioni hello hello repository toobuild ed eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="38f4c-191">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="38f4c-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="38f4c-192">Errore imprevisto durante il tentativo di tooopen una connessione SQL</span><span class="sxs-lookup"><span data-stu-id="38f4c-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="38f4c-193">**Sintomi**: durante la connessione cluster HDInsight tooan versione 3.3 o 3.4, si potrebbe ricevere un errore che si è verificato un errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="38f4c-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="38f4c-194">analisi dello stack dell'errore Hello inizia con hello seguenti righe:</span><span class="sxs-lookup"><span data-stu-id="38f4c-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="38f4c-195">**Causa**: questo errore è causato da una mancata corrispondenza nella versione di hello hello commons codec.jar del file di utilizzato esce e hello uno necessario per i componenti Hive JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="38f4c-196">**Risoluzione**: toofix questo errore, utilizzare hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="38f4c-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="38f4c-197">Scaricare il file jar commons codec hello dal cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="38f4c-198">Chiudere esce e quindi passare toohello directory in cui esce è installato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="38f4c-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="38f4c-199">Nella directory esce hello in hello `lib` directory, sostituire hello esistente commons-codec.jar con download di uno dal cluster HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="38f4c-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="38f4c-200">Riavviare SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="38f4c-200">Restart SQuirreL.</span></span> <span data-ttu-id="38f4c-201">Errore di Hello non deve verificarsi quando ci si connette tooHive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f4c-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38f4c-202">Next steps</span></span>

<span data-ttu-id="38f4c-203">Ora che si è appreso come toouse JDBC toowork con Hive, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38f4c-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="38f4c-204">Caricare dati tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="38f4c-205">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="38f4c-206">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="38f4c-207">Usare processi MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="38f4c-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
