---
title: strumenti di aaaData Lake per Visual Studio con Hortonworks Sandbox - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello strumenti di Azure Data Lake per Visual Studio con sandbox Hortonworks hello in esecuzione in una macchina virtuale locale. Con questi strumenti, è possibile creare ed eseguire i processi Hive e Pig sandbox hello e visualizzare l'output processo e della cronologia."
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
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="d9ba0-104">Utilizzare gli strumenti di Azure Data Lake hello per Visual Studio con hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="d9ba0-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="d9ba0-105">Azure Data Lake include strumenti per l'uso di cluster Hadoop generici.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="d9ba0-106">Questo documento vengono illustrate operazioni di hello necessari gli strumenti di Data Lake hello toouse con hello Hortonworks Sandbox in esecuzione in una macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="d9ba0-107">Utilizzo di hello Hortonworks Sandbox consente toowork con Hadoop in ambiente di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="d9ba0-108">Dopo aver sviluppato una soluzione e si desidera toodeploy è su larga scala, è quindi possibile spostare il cluster di HDInsight tooan.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9ba0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d9ba0-109">Prerequisites</span></span>

* <span data-ttu-id="d9ba0-110">Hello Hortonworks Sandbox, in esecuzione in una macchina virtuale in un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="d9ba0-111">Questo documento è stato scritto e testato con sandbox hello in esecuzione in Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="d9ba0-112">Per informazioni sull'impostazione della sandbox hello, vedere hello [introduzione sandbox Hortonworks hello.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="d9ba0-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="d9ba0-113">nel relativo documento.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-113">document.</span></span>

* <span data-ttu-id="d9ba0-114">Visual Studio 2013, Visual Studio 2015 o Visual Studio 2017 (qualsiasi edizione).</span><span class="sxs-lookup"><span data-stu-id="d9ba0-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="d9ba0-115">Hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/) 2.7.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="d9ba0-116">Hello [di strumenti di Azure Data Lake per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="d9ba0-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="d9ba0-117">Configurare le password per il sandbox hello</span><span class="sxs-lookup"><span data-stu-id="d9ba0-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="d9ba0-118">Verificare che tale hello che hortonworks Sandbox è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="d9ba0-119">Seguire i passaggi di hello in hello [iniziare a utilizzare hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="d9ba0-120">Questi passaggi configurare password hello per hello SSH `root` account e hello Ambari `admin` account.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="d9ba0-121">Le password vengono utilizzate quando ci si connette toohello sandbox da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="d9ba0-122">Connettersi sandbox di hello strumenti toohello</span><span class="sxs-lookup"><span data-stu-id="d9ba0-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="d9ba0-123">Aprire Visual Studio, selezionare **Visualizza** e quindi **Esplora server**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="d9ba0-124">Da **Esplora Server**, hello rapida **HDInsight** voce e quindi selezionare **connettersi tooHDInsight emulatore**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Schermata di Esplora Server con connessione tooHDInsight emulatore evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="d9ba0-126">Da hello **connettersi tooHDInsight emulatore** finestra di dialogo immettere hello password configurata per Ambari.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="d9ba0-128">Selezionare **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="d9ba0-129">Hello utilizzare **Password** password di hello tooenter campo configurati per hello `root` account.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="d9ba0-130">Lasciare hello altri campi al valore predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-130">Leave hello other fields at hello default value.</span></span>

    ![Schermata della finestra di dialogo, con casella di testo della password evidenziata](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="d9ba0-132">Selezionare **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="d9ba0-133">Attesa per la convalida di hello servizi toofinish.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="d9ba0-134">In alcuni casi, la convalida potrebbe avere esito negativo e viene configurazione hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="d9ba0-135">Se la convalida non riesce, selezionare **aggiornamento**e attendere la verifica per toofinish servizio hello e configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Schermata della finestra di dialogo, con il pulsante Aggiorna evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="d9ba0-137">il processo di aggiornamento di Hello utilizza hello toomodify Ambari toowhat configurazione Hortonworks Sandbox previsto dagli strumenti di Data Lake hello per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="d9ba0-138">Al termine della convalida, selezionare **fine** toocomplete configurazione.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="d9ba0-139">![Schermata della finestra di dialogo, con il pulsante Fine evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="d9ba0-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="d9ba0-140">A seconda della velocità di hello dell'ambiente di sviluppo e hello quantità di memoria allocata macchina virtuale toohello, può richiedere diversi minuti tooconfigure e convalidare i servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="d9ba0-141">Dopo aver completato questi passaggi, è ora un **cluster locale di HDInsight** voce in Esplora Server, hello **HDInsight** sezione.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="d9ba0-142">Scrivere una query Hive</span><span class="sxs-lookup"><span data-stu-id="d9ba0-142">Write a Hive query</span></span>

<span data-ttu-id="d9ba0-143">Hive fornisce un linguaggio di query simile a SQL (HiveQL) per la gestione dei dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="d9ba0-144">Utilizzare hello seguendo i passaggi toolearn come una query sul cluster locale hello toorun su richiesta.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="d9ba0-145">In **Esplora Server**, fare clic sulla voce hello per cluster locale hello aggiunto in precedenza e quindi selezionare **scrivere una Query Hive**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Schermata di Esplora server, con Scrivi una query Hive evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="d9ba0-147">Verrà visualizzata una nuova finestra di query,</span><span class="sxs-lookup"><span data-stu-id="d9ba0-147">A new query window appears.</span></span> <span data-ttu-id="d9ba0-148">Qui è possibile scrivere e inviare un cluster locale toohello di query.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="d9ba0-149">Nella nuova finestra query di hello, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d9ba0-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="d9ba0-150">la query toorun hello, seleziona **Invia** nella parte superiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="d9ba0-151">Lasciare gli altri valori di hello (**Batch** e nome del server) in valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Schermata della finestra di query, con il pulsante di invio hello evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="d9ba0-153">È inoltre possibile utilizzare il menu di scelta rapida hello accanto troppo**Invia** tooselect **avanzate**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="d9ba0-154">Le opzioni avanzate consentono di opzioni aggiuntive tooprovide quando si invia il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="d9ba0-156">Dopo aver inviato query hello, viene visualizzato lo stato del processo hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="d9ba0-157">lo stato del processo Hello Visualizza informazioni sul processo hello viene elaborato da Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="d9ba0-158">**Lo stato del processo** fornisce hello lo stato del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="d9ba0-159">lo stato di Hello viene aggiornato periodicamente oppure è possibile utilizzare hello aggiornare icona toorefresh hello lo stato manualmente.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Schermata della finestra di dialogo Vista processi con Stato processo evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="d9ba0-161">Dopo hello **lo stato del processo** cambia troppo**completato**, viene visualizzato un indirizzate aciclico Graph (DAG).</span><span class="sxs-lookup"><span data-stu-id="d9ba0-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="d9ba0-162">Questo diagramma illustra percorso di esecuzione hello che è stato determinato dal Tez durante l'elaborazione di query Hive hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="d9ba0-163">Tez è di tipo motore di esecuzione predefinito hello per Hive nel cluster locale hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9ba0-164">Tez è predefinito hello quando si utilizza il cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="d9ba0-165">Non è predefinita hello in HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="d9ba0-166">toouse è disponibile, è necessario aggiungere la riga hello `set hive.execution.engine = tez;` toohello inizio della query Hive.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="d9ba0-167">Hello utilizzare **Output processo** collegamento di output di hello tooview.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="d9ba0-168">In questo caso, è 823, numero hello di righe nella tabella sample_08 hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="d9ba0-169">È possibile visualizzare informazioni diagnostiche sul processo hello utilizzando hello **Log processo** e **Scarica Log di YARN** collegamenti.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="d9ba0-170">È anche possibile eseguire in modo interattivo i processi Hive modificando hello **Batch** campo troppo**Interactive**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="d9ba0-171">quindi selezionando **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-171">Then select **Execute**.</span></span>

    ![Schermata dei pulsanti Interattivo ed Esecuzione evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="d9ba0-173">Una query interattiva flussi hello log di output generato durante l'elaborazione toohello **HiveServer2 Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9ba0-174">Hello informazioni è hello uguale a quello disponibile dalla hello **Log processo** termine un processo di collegamento.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Schermata del log di output](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="d9ba0-176">Creare un progetto Hive</span><span class="sxs-lookup"><span data-stu-id="d9ba0-176">Create a Hive project</span></span>

<span data-ttu-id="d9ba0-177">Inoltre, è possibile creare un progetto che contiene più script Hive.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="d9ba0-178">Utilizzare un progetto quando si dispone di script correlati o gli script toostore in un sistema di controllo della versione.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="d9ba0-179">In Visual Studio selezionare **File**, **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="d9ba0-180">Elenco di progetti hello espandere **modelli**, espandere **Azure Data Lake**, quindi selezionare **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="d9ba0-181">Selezionare nell'elenco dei modelli di hello **esempio Hive**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="d9ba0-182">Immettere un nome e un percorso e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-182">Enter a name and location, and then select **OK**.</span></span>

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, HIVE, Hive Sample e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="d9ba0-184">Hello **esempio Hive** progetto contiene due script, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="d9ba0-185">È possibile inviare questi script utilizzando hello stesso **Invia** pulsante nella parte superiore di hello della finestra hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="d9ba0-186">Creare un progetto Pig</span><span class="sxs-lookup"><span data-stu-id="d9ba0-186">Create a Pig project</span></span>

<span data-ttu-id="d9ba0-187">Mentre Hive offre un linguaggio simile a SQL per la gestione dei dati strutturati, Pig esegue trasformazioni sui dati.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="d9ba0-188">Pig fornisce un linguaggio (alfabeto latino Pig) che consente di toodevelop una pipeline di trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="d9ba0-189">toouse Pig con cluster locale hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d9ba0-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="d9ba0-190">Aprire Visual Studio e selezionare **File** **Nuovo** e quindi **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="d9ba0-191">Elenco di progetti hello espandere **modelli**, espandere **Azure Data Lake**, quindi selezionare **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="d9ba0-192">Selezionare nell'elenco dei modelli di hello **Pig applicazione**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="d9ba0-193">Immettere un nome e un percorso e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-193">Enter a name, location, and then select **OK**.</span></span>

    ![Screenshot della finestra Nuovo progetto, con Azure Data Lake, Pig, Pig Application e OK evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="d9ba0-195">Immettere di seguito il testo come contenuto di hello di hello hello **script.pig** file che è stato creato con questo progetto.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="d9ba0-196">Sebbene di Hive, Pig utilizza una lingua diversa, le modalità di esecuzione di processi di hello è coerente tra entrambi i linguaggi, tramite hello **Invia** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="d9ba0-197">Hello Seleziona elenco a discesa accanto a **Invia** consente di visualizzare la finestra di dialogo di invio avanzate per Pig.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Schermata della finestra di dialogo Invia Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="d9ba0-199">Hello lo stato del processo e viene anche visualizzato l'output di hello stesso come una query Hive.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Screenshot di un processo Pig completato](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="d9ba0-201">Visualizzare i processi</span><span class="sxs-lookup"><span data-stu-id="d9ba0-201">View jobs</span></span>

<span data-ttu-id="d9ba0-202">Data Lake consentono inoltre tooeasily Visualizza informazioni sui processi che sono state eseguite in Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="d9ba0-203">Utilizzare hello seguendo i processi di hello toosee passaggi che sono stati eseguiti nel cluster locale hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="d9ba0-204">Da **Esplora Server**, cluster locale hello e quindi scegliere **Visualizza processi**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="d9ba0-205">Viene visualizzato un elenco di processi che sono stati inviati toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Schermata di Esplora Server, con Visualizza processi evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="d9ba0-207">Elenco di hello dei processi, selezionare una tooview i dettagli dei processi hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Schermata di processo Browser, con uno dei processi di hello evidenziati](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="d9ba0-209">informazioni di Hello visualizzate sono simili toowhat che vengono visualizzati dopo l'esecuzione di una query Hive o Pig, inclusi i collegamenti tooview hello output e informazioni di registrazione.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="d9ba0-210">È inoltre possibile modificare e quindi inviare nuovamente il processo di hello da qui.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="d9ba0-211">Visualizzare i database Hive</span><span class="sxs-lookup"><span data-stu-id="d9ba0-211">View Hive databases</span></span>

1. <span data-ttu-id="d9ba0-212">In **Esplora Server**, espandere hello **cluster locale di HDInsight** voce, quindi espandere **database Hive**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="d9ba0-213">Hello **predefinito** e **xademo** i database nel cluster locale hello vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="d9ba0-214">Espansione di un database Mostra tabelle hello hello database.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Schermata di Esplora server, con i database espansi](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="d9ba0-216">Espandendo una tabella consente di visualizzare le colonne di hello per la tabella.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="d9ba0-217">tooquickly visualizzare i dati hello, una tabella e scegliere **Visualizza le prime 100 righe**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Schermata di Esplora server con tabella espansa e opzione Visualizza prime 100 righe selezionata](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="d9ba0-219">Proprietà del database e della tabella</span><span class="sxs-lookup"><span data-stu-id="d9ba0-219">Database and table properties</span></span>

<span data-ttu-id="d9ba0-220">È possibile visualizzare le proprietà di hello del database o tabella.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="d9ba0-221">Selezione **proprietà** consente di visualizzare i dettagli per l'elemento hello selezionato nella finestra Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="d9ba0-222">Ad esempio, vedere informazioni hello mostrate nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="d9ba0-222">For example, see hello information shown in hello following screenshot:</span></span>

![Schermata della finestra Proprietà](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="d9ba0-224">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="d9ba0-224">Create a table</span></span>

<span data-ttu-id="d9ba0-225">toocreate una tabella, fare doppio clic su un database e quindi selezionare **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Schermata di Esplora Server, con Crea tabella evidenziato](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="d9ba0-227">È quindi possibile creare una tabella di hello tramite un modulo.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-227">You can then create hello table using a form.</span></span> <span data-ttu-id="d9ba0-228">Nella parte inferiore di hello di hello seguente schermata, è possibile visualizzare hello HiveQL non elaborate che è usato toocreate hello tabella.</span><span class="sxs-lookup"><span data-stu-id="d9ba0-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Schermata di form hello utilizzato toocreate una tabella](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="d9ba0-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9ba0-230">Next steps</span></span>

* [<span data-ttu-id="d9ba0-231">Cavi hello di apprendimento di hello Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="d9ba0-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="d9ba0-232">Esercitazione di Hadoop: introduzione a HDP</span><span class="sxs-lookup"><span data-stu-id="d9ba0-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
