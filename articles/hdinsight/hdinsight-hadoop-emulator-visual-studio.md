---
title: Strumenti Data Lake per Visual Studio con Hortonworks Sandbox - HDInsight di Azure | Documentazione Microsoft
description: "Informazioni su come usare gli strumenti Azure Data Lake per VIsual Studio con Sandbox di Hortonworks (in esecuzione su una macchina virtuale locale). Grazie a questi strumenti è possibile creare ed eseguire i processi Hive e Pig in Sandbox, oltre a visualizzare l'output del processo e la cronologia."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="7910a-104">Usare gli strumenti Azure Data Lake per Visual Studio con Sandbox di Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7910a-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="7910a-105">Azure Data Lake include strumenti per l'uso di cluster Hadoop generici.</span><span class="sxs-lookup"><span data-stu-id="7910a-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="7910a-106">Questo documento illustra la procedura necessaria per l'uso degli strumenti Data Lake con Hortonworks Sandbox in esecuzione in una macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="7910a-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="7910a-107">Sandbox di Hortonworks consente di utilizzare Hadoop in locale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="7910a-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="7910a-108">Dopo aver sviluppato una soluzione da distribuire in modo scalabile, è possibile passare a un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7910a-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7910a-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7910a-109">Prerequisites</span></span>

* <span data-ttu-id="7910a-110">Sandbox di Hortonworks in esecuzione su una macchina virtuale nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="7910a-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="7910a-111">Questo documento è stato scritto e testato con l'ambiente sandbox in esecuzione in Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="7910a-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="7910a-112">Per informazioni sulla configurazione della sandbox, vedere l'[introduzione a Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7910a-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="7910a-113">nel relativo documento.</span><span class="sxs-lookup"><span data-stu-id="7910a-113">document.</span></span>

* <span data-ttu-id="7910a-114">Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (qualsiasi edizione).</span><span class="sxs-lookup"><span data-stu-id="7910a-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="7910a-115">[Azure SDK per .NET](https://azure.microsoft.com/downloads/) 2.7.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7910a-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="7910a-116">Gli [strumenti Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="7910a-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="7910a-117">Configurare le password per Sandbox</span><span class="sxs-lookup"><span data-stu-id="7910a-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="7910a-118">Assicurarsi che l'ambiente Hortonworks Sandbox sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7910a-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="7910a-119">Seguire la proceduta illustrata nel documento di [introduzione a Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords).</span><span class="sxs-lookup"><span data-stu-id="7910a-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="7910a-120">per configurare la password dell'account `root` SSH e dell'account `admin` Ambari.</span><span class="sxs-lookup"><span data-stu-id="7910a-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="7910a-121">Queste password vengono usate per la connessione a Sandbox da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7910a-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="7910a-122">Connettere gli strumenti a Sandbox</span><span class="sxs-lookup"><span data-stu-id="7910a-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="7910a-123">Aprire Visual Studio, selezionare **Visualizza** e quindi **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="7910a-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="7910a-124">In **Esplora server** fare clic con il pulsante destro del mouse sulla voce **HDInsight** e quindi scegliere **Connect to HDInsight Emulator** (Connetti a HDInsight Emulator).</span><span class="sxs-lookup"><span data-stu-id="7910a-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Schermata di Esplora Server con Connetti a HDInsight Emulator evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="7910a-126">Nella finestra di dialogo **Connect to HDInsight Emulator** (Connetti a HDInsight Emulator) immettere la password configurata per Ambari.</span><span class="sxs-lookup"><span data-stu-id="7910a-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="7910a-128">Selezionare **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="7910a-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="7910a-129">Usare il campo **Password** per immettere la password configurata per l'account `root`.</span><span class="sxs-lookup"><span data-stu-id="7910a-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="7910a-130">Mantenere i valori predefiniti per gli altri campi.</span><span class="sxs-lookup"><span data-stu-id="7910a-130">Leave the other fields at the default value.</span></span>

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="7910a-132">Selezionare **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="7910a-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="7910a-133">Attendere il completamento della convalida dei servizi.</span><span class="sxs-lookup"><span data-stu-id="7910a-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="7910a-134">In alcuni casi, la convalida potrebbe non riuscire e verrebbe chiesto di aggiornare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7910a-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="7910a-135">Se la convalida ha esito negativo, selezionare il pulsante **Aggiorna** e attendere il completamento della configurazione e della verifica del servizio.</span><span class="sxs-lookup"><span data-stu-id="7910a-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![Schermata della finestra di dialogo, con il pulsante Aggiorna evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="7910a-137">Il processo di aggiornamento usa Ambari per modificare la configurazione di Hortonworks Sandbox su quella prevista dagli strumenti Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7910a-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="7910a-138">Al termine della convalida, selezionare **Fine** per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7910a-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="7910a-139">![Schermata della finestra di dialogo, con il pulsante Fine evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="7910a-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="7910a-140">A seconda della velocità dell'ambiente di sviluppo e della quantità di memoria allocata sulla macchina virtuale, la configurazione e la convalida dei servizi potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="7910a-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="7910a-141">Al termine della procedura indicata, si dispone di una voce **Cluster locale HDInsight** in Esplora server nella sezione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7910a-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="7910a-142">Scrivere una query Hive</span><span class="sxs-lookup"><span data-stu-id="7910a-142">Write a Hive query</span></span>

<span data-ttu-id="7910a-143">Hive fornisce un linguaggio di query simile a SQL (HiveQL) per la gestione dei dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="7910a-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="7910a-144">Per informazioni su come eseguire query a richiesta nel cluster locale, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="7910a-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="7910a-145">In **Esplora server** fare clic con il pulsante destro del mouse sulla voce del cluster locale aggiunto in precedenza e quindi scegliere **Scrivi una query Hive**.</span><span class="sxs-lookup"><span data-stu-id="7910a-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Schermata di Esplora server, con Scrivi una query Hive evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="7910a-147">Verrà visualizzata una nuova finestra di query,</span><span class="sxs-lookup"><span data-stu-id="7910a-147">A new query window appears.</span></span> <span data-ttu-id="7910a-148">utilizzabile per scrivere e inviare una query al cluster locale.</span><span class="sxs-lookup"><span data-stu-id="7910a-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="7910a-149">Nella nuova finestra di query immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7910a-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="7910a-150">Per eseguire la query, selezionare **Invia** nella parte superiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="7910a-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="7910a-151">Mantenere i valori predefiniti negli altri campi (**Batch** e nome del server).</span><span class="sxs-lookup"><span data-stu-id="7910a-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![Schermata della finestra di query, con il pulsante Invia evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="7910a-153">È anche possibile usare il menu a discesa accanto a **Invia** per selezionare **Avanzate**.</span><span class="sxs-lookup"><span data-stu-id="7910a-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="7910a-154">In questo modo è possibile specificare opzioni aggiuntive durante l'invio del processo.</span><span class="sxs-lookup"><span data-stu-id="7910a-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="7910a-156">Dopo aver inviato la query viene visualizzato lo stato del processo,</span><span class="sxs-lookup"><span data-stu-id="7910a-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="7910a-157">che fornisce informazioni sul processo mentre viene elaborato da Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7910a-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="7910a-158">La voce **Stato processo** indica lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="7910a-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="7910a-159">Anche se lo stato viene aggiornato periodicamente, è possibile usare l'icona di aggiornamento per eseguire l'operazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="7910a-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![Schermata della finestra di dialogo Vista processi con Stato processo evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="7910a-161">Quando **Stato processo** diventa **Terminato**, viene visualizzato un grafo aciclico diretto (DAG).</span><span class="sxs-lookup"><span data-stu-id="7910a-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="7910a-162">Questo diagramma descrive il percorso di esecuzione determinato da Tez durante l'elaborazione della query Hive.</span><span class="sxs-lookup"><span data-stu-id="7910a-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="7910a-163">Tez è il motore di esecuzione predefinito per Hive nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="7910a-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7910a-164">Tez è anche il motore predefinito quando si usano i cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="7910a-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="7910a-165">Non è il valore predefinito in HDInsight basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="7910a-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="7910a-166">Per usarlo su Windows è necessario aggiungere la riga `set hive.execution.engine = tez;` all'inizio della query Hive.</span><span class="sxs-lookup"><span data-stu-id="7910a-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="7910a-167">Usare il collegamento **Job Output** (Output processo) per visualizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="7910a-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="7910a-168">In questo caso è 823, il numero di righe nella tabella sample_08.</span><span class="sxs-lookup"><span data-stu-id="7910a-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="7910a-169">È possibile visualizzare le informazioni di diagnostica relative al processo usando i collegamenti **Job Log** (Log processo) e **Download YARN Log** (Scarica log YARN).</span><span class="sxs-lookup"><span data-stu-id="7910a-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="7910a-170">È anche possibile eseguire in modo interattivo i processi Hive impostando il campo **Batch** su **Interattivo**,</span><span class="sxs-lookup"><span data-stu-id="7910a-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="7910a-171">quindi selezionando **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="7910a-171">Then select **Execute**.</span></span>

    ![Schermata dei pulsanti Interattivo ed Esecuzione evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="7910a-173">Una query interattiva trasmette il log di output generato durante l'elaborazione alla finestra **Output HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="7910a-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7910a-174">Si tratta delle stesse informazioni accessibili dal collegamento **Log processo** dopo il completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="7910a-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![Schermata del log di output](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="7910a-176">Creare un progetto Hive</span><span class="sxs-lookup"><span data-stu-id="7910a-176">Create a Hive project</span></span>

<span data-ttu-id="7910a-177">Inoltre, è possibile creare un progetto che contiene più script Hive.</span><span class="sxs-lookup"><span data-stu-id="7910a-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="7910a-178">Usare un progetto quando si hanno script correlati o si vogliono archiviare gli script in un sistema di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="7910a-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="7910a-179">In Visual Studio selezionare **File**, **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="7910a-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="7910a-180">Nell'elenco dei progetti espandere **Modelli** e **Azure Data Lake**, quindi selezionare **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="7910a-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="7910a-181">Nell'elenco dei modelli selezionare **Hive Sample** (Esempio Hive).</span><span class="sxs-lookup"><span data-stu-id="7910a-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="7910a-182">Immettere un nome e un percorso e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="7910a-182">Enter a name and location, and then select **OK**.</span></span>

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, HIVE, Hive Sample e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="7910a-184">Il progetto **Hive Sample** (Esempio Hive) contiene due script, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="7910a-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="7910a-185">È possibile inviare gli script usando lo stesso pulsante **Invia** nella parte superiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="7910a-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="7910a-186">Creare un progetto Pig</span><span class="sxs-lookup"><span data-stu-id="7910a-186">Create a Pig project</span></span>

<span data-ttu-id="7910a-187">Mentre Hive offre un linguaggio simile a SQL per la gestione dei dati strutturati, Pig esegue trasformazioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="7910a-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="7910a-188">Pig offre infatti un linguaggio (Pig Latin) che consente di sviluppare una pipeline di trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="7910a-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="7910a-189">Per usare Pig con il cluster locale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7910a-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="7910a-190">Aprire Visual Studio e selezionare **File** **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="7910a-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="7910a-191">Nell'elenco dei progetti espandere **Modelli** e **Azure Data Lake** e quindi selezionare **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="7910a-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="7910a-192">Nell'elenco dei modelli selezionare **Pig Application** (Applicazione Pig).</span><span class="sxs-lookup"><span data-stu-id="7910a-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="7910a-193">Immettere un nome e un percorso e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="7910a-193">Enter a name, location, and then select **OK**.</span></span>

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, Pig, Pig Application e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="7910a-195">Immettere il testo seguente come contenuto del file **script.pig** creato con questo progetto.</span><span class="sxs-lookup"><span data-stu-id="7910a-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="7910a-196">Nonostante Pig usi un linguaggio diverso rispetto a Hive, la modalità di esecuzione dei processi si mantiene coerente tra entrambi i linguaggi tramite il pulsante **Invia**.</span><span class="sxs-lookup"><span data-stu-id="7910a-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="7910a-197">Selezionando l'elenco a discesa accanto a **Invia** viene visualizzata una finestra di dialogo di invio avanzato per Pig.</span><span class="sxs-lookup"><span data-stu-id="7910a-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="7910a-199">Anche lo stato del processo e l'output vengono visualizzati allo stesso modo di una query Hive.</span><span class="sxs-lookup"><span data-stu-id="7910a-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![Screenshot di un processo Pig completato](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="7910a-201">Visualizzare i processi</span><span class="sxs-lookup"><span data-stu-id="7910a-201">View jobs</span></span>

<span data-ttu-id="7910a-202">Gli strumenti Data Lake consentono anche di visualizzare facilmente le informazioni sui processi che sono stati eseguiti in Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7910a-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="7910a-203">Usare la procedura seguente per visualizzare i processi che sono stati eseguiti nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="7910a-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="7910a-204">In **Esplora server** fare clic con il pulsante destro del mouse sul cluster locale e quindi scegliere **Visualizza processi**</span><span class="sxs-lookup"><span data-stu-id="7910a-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="7910a-205">per aprire l'elenco dei processi che sono stati inviati al cluster.</span><span class="sxs-lookup"><span data-stu-id="7910a-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![Schermata di Esplora Server, con Visualizza processi evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="7910a-207">Da questo elenco, selezionare un processo per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="7910a-207">From the list of jobs, select one to view the job details.</span></span>

    ![Schermata di Browser processi, con uno dei processi evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="7910a-209">Le informazioni visualizzate sono simili a quelle che appaiono dopo l'esecuzione di una query Hive o Pig, inclusi i collegamenti per visualizzare le informazioni relative al log e all'output.</span><span class="sxs-lookup"><span data-stu-id="7910a-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="7910a-210">Da qui si può anche modificare il processo e inviarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="7910a-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="7910a-211">Visualizzare i database Hive</span><span class="sxs-lookup"><span data-stu-id="7910a-211">View Hive databases</span></span>

1. <span data-ttu-id="7910a-212">In **Esplora server** espandere la voce **HDInsight local cluster** (Cluster locale HDInsight) e quindi **Hive Databases** (Database Hive).</span><span class="sxs-lookup"><span data-stu-id="7910a-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="7910a-213">Verranno visualizzati i database **Default** e **xademo** nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="7910a-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="7910a-214">Attraverso l'espansione di un database è possibile visualizzare le tabelle al suo interno.</span><span class="sxs-lookup"><span data-stu-id="7910a-214">Expanding a database shows the tables within the database.</span></span>

    ![Schermata di Esplora server, con i database espansi](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="7910a-216">L'espansione della consente di visualizzare le colonne presenti in essa.</span><span class="sxs-lookup"><span data-stu-id="7910a-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="7910a-217">Per visualizzare rapidamente i dati fare clic con il pulsante destro del mouse su una tabella e scegliere **Visualizza prime 100 righe**.</span><span class="sxs-lookup"><span data-stu-id="7910a-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Schermata di Esplora server con tabella espansa e opzione Visualizza prime 100 righe selezionata](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="7910a-219">Proprietà del database e della tabella</span><span class="sxs-lookup"><span data-stu-id="7910a-219">Database and table properties</span></span>

<span data-ttu-id="7910a-220">È possibile visualizzare le proprietà di un database o di una tabella</span><span class="sxs-lookup"><span data-stu-id="7910a-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="7910a-221">in modo da mostrare i dettagli per l'elemento selezionato nella finestra **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="7910a-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="7910a-222">Vedere ad esempio le informazioni visualizzate nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7910a-222">For example, see the information shown in the following screenshot:</span></span>

![Schermata della finestra Proprietà](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="7910a-224">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="7910a-224">Create a table</span></span>

<span data-ttu-id="7910a-225">Per creare una tabella, fare clic con il pulsante destro del mouse su un database e quindi scegliere **Crea tabella**.</span><span class="sxs-lookup"><span data-stu-id="7910a-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![Schermata di Esplora Server, con Crea tabella evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="7910a-227">È quindi possibile creare la tabella utilizzando un modulo.</span><span class="sxs-lookup"><span data-stu-id="7910a-227">You can then create the table using a form.</span></span> <span data-ttu-id="7910a-228">Nella parte inferiore della schermata seguente è possibile visualizzare il codice HiveQL non elaborato che verrà usato per creare la tabella.</span><span class="sxs-lookup"><span data-stu-id="7910a-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![Schermata del modulo usato per creare una tabella](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="7910a-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7910a-230">Next steps</span></span>

* [<span data-ttu-id="7910a-231">Acquisire dimestichezza con Sandbox di Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7910a-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="7910a-232">Esercitazione di Hadoop: introduzione a HDP</span><span class="sxs-lookup"><span data-stu-id="7910a-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
