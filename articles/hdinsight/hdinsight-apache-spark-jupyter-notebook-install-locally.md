---
title: aaaInstall Jupyter localmente & connettere il cluster di Azure HDInsight Spark tooan | Documenti Microsoft
description: Informazioni su come tooinstall server Jupyter notebook in locale nel computer e connetterla tooan cluster Apache Spark in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="b2ec4-103">Installare server Jupyter notebook nel computer e connettere tooApache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="b2ec4-104">In questo articolo viene illustrato come tooinstall server Jupyter notebook, hello PySpark personalizzato (per Python) e kernel Spark (per la Scala) con nascita magic e connettere i cluster di HDInsight tooan notebook hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="b2ec4-105">Può esistere un numero di motivi tooinstall Jupyter sul computer locale e possono essere presenti anche alcune problematiche.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="b2ec4-106">Per ulteriori informazioni, vedere la sezione hello [perché è consigliabile installare Jupyter computer](#why-should-i-install-jupyter-on-my-computer) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="b2ec4-107">Sono disponibili tre passaggi chiavi per l'installazione di server Jupyter e hello magic Spark nel computer.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="b2ec4-108">Installare Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="b2ec4-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="b2ec4-109">Installare hello PySpark e directcompute Spark con hello magic Spark</span><span class="sxs-lookup"><span data-stu-id="b2ec4-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="b2ec4-110">Configurare Spark magic tooaccess cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="b2ec4-111">Per ulteriori informazioni su kernel personalizzata hello e magic Spark hello disponibili per notebook Jupyter con cluster HDInsight, vedere [kernel disponibile per i server Jupyter notebook con Apache Spark Linux cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2ec4-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b2ec4-112">Prerequisites</span></span>
<span data-ttu-id="b2ec4-113">prerequisiti di Hello elencati di seguito non sono presenti per l'installazione Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="b2ec4-114">Si tratta per il cluster HDInsight connessione hello Jupyter notebook tooan dopo aver installato notebook hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="b2ec4-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-115">An Azure subscription.</span></span> <span data-ttu-id="b2ec4-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b2ec4-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b2ec4-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="b2ec4-119">Installare Jupyter Notebook nel computer</span><span class="sxs-lookup"><span data-stu-id="b2ec4-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="b2ec4-120">Prima di installare i notebook Jupyter è necessario installare Python.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="b2ec4-121">Python e Jupyter sono entrambe disponibili come parte di hello [distribuzione Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="b2ec4-122">Quando si installa Anaconda, viene installata una distribuzione di Python.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="b2ec4-123">Una volta installato Anaconda, aggiungere installazione Jupyter hello eseguendo i comandi appropriati.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="b2ec4-124">Scaricare hello [installer Anaconda](https://www.continuum.io/downloads) per la piattaforma e il programma di installazione di hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="b2ec4-125">Durante l'installazione guidata in esecuzione hello, assicurarsi di selezionare variabile PATH di hello opzione tooadd Anaconda tooyour.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="b2ec4-126">Comando che segue di esecuzione hello tooinstall Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="b2ec4-127">Per altre informazioni sull'installazione di Jupyter, vedere l'argomento relativo all' [installazione di Jupyter mediante Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="b2ec4-128">Installare kernel hello e magic Spark</span><span class="sxs-lookup"><span data-stu-id="b2ec4-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="b2ec4-129">Per istruzioni su come magic di Spark hello tooinstall, hello PySpark e kernel Spark, seguire le istruzioni di installazione hello in hello [sparkmagic documentazione](https://github.com/jupyter-incubator/sparkmagic#installation) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="b2ec4-130">Hello primo passaggio nella documentazione di magic Spark hello chiesto magic Spark tooinstall.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="b2ec4-131">Sostituire il primo passaggio nel collegamento hello con hello seguenti comandi, a seconda della versione di hello del cluster HDInsight hello che ci si connetterà.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="b2ec4-132">Successivamente, seguire hello rimanenti passaggi nella documentazione di magic Spark hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="b2ec4-133">Se si desidera kernel di tooinstall hello differenti, è necessario eseguire il passaggio 3 nella sezione di istruzioni di installazione magic Spark hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="b2ec4-134">Per i cluster v3.4, installare sparkmagic 0.2.3 eseguendo `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="b2ec4-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="b2ec4-135">Per i cluster v3.5 e v3.6, installare sparkmagic 0.11.2 eseguendo `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="b2ec4-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="b2ec4-136">Configurare cluster di Spark tooHDInsight tooconnect magic Spark</span><span class="sxs-lookup"><span data-stu-id="b2ec4-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="b2ec4-137">In questa sezione è configurare magic Spark hello installato cluster Apache Spark tooan precedenti tooconnect che è necessario avere già creato in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="b2ec4-138">informazioni di configurazione Jupyter Hello è in genere archiviato nella home directory di hello gli utenti.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="b2ec4-139">toolocate comandi della home directory in qualsiasi piattaforma del sistema operativo, hello tipo seguente.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="b2ec4-140">Avviare shell di Python hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-140">Start hello Python shell.</span></span> <span data-ttu-id="b2ec4-141">In una finestra di comando digitare seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b2ec4-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="b2ec4-142">Nella shell di Python hello, immettere hello successivo comando toofind home directory di hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="b2ec4-143">Passare toohello home directory e creare una cartella denominata **.sparkmagic** se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="b2ec4-144">Nella cartella hello, creare un file denominato **config. JSON** e aggiungere hello seguente frammento di codice JSON all'interno.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="b2ec4-145">Sostituire **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="b2ec4-146">È possibile utilizzare un numero di utilità il linguaggio di programmazione preferito o la password con codifica base64 di toogenerate online per la password effettiva.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="b2ec4-147">Configurare impostazioni Heartbeat corrette hello in `config.json`.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="b2ec4-148">È necessario aggiungere queste impostazioni in hello stesso livello come hello `kernel_python_credentials` e `kernel_scala_credentials` frammenti di codice le aggiunte in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="b2ec4-149">Per un esempio di come e dove tooadd hello le impostazioni di heartbeat, vedere questo [config. JSON di esempio](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="b2ec4-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="b2ec4-150">Per `sparkmagic 0.2.3` (cluster v3.4), includere:</span><span class="sxs-lookup"><span data-stu-id="b2ec4-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="b2ec4-151">Per `sparkmagic 0.11.2` (cluster v3.5 e v3.6), includere:</span><span class="sxs-lookup"><span data-stu-id="b2ec4-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="b2ec4-152">Tooensure che le sessioni non vengono comunicate vengono inviati heartbeat.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="b2ec4-153">Quando un computer passa toosleep o è stato arrestato, non vengono inviati heartbeat hello, risultante in corso di sessione hello puliti.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="b2ec4-154">Per i cluster v3.4, se si desidera toodisable questo comportamento, è possibile impostare hello configurazione inserire il `livy.server.interactive.heartbeat.timeout` troppo`0` da hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="b2ec4-155">Per la versione 3.5 di cluster, se non si imposta configurazione hello 3.5 precedente, la sessione hello non verrà eliminata.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="b2ec4-156">Avviare Jupyter.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-156">Start Jupyter.</span></span> <span data-ttu-id="b2ec4-157">Utilizzare hello comando seguente dal prompt dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="b2ec4-158">Verificare che sia possibile connettersi toohello cluster utilizzando notebook Jupyter hello e che è possibile utilizzare magic Spark hello disponibile con il kernel hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="b2ec4-159">Eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-159">Perform hello following steps.</span></span>

    <span data-ttu-id="b2ec4-160">a.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-160">a.</span></span> <span data-ttu-id="b2ec4-161">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-161">Create a new notebook.</span></span> <span data-ttu-id="b2ec4-162">Nell'angolo destro hello, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="b2ec4-163">Dovrebbe essere kernel predefinito hello **Python2** e hello due directcompute nuova che si installano, **PySpark** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="b2ec4-164">Fare clic su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-164">Click **PySpark**.</span></span>

    <span data-ttu-id="b2ec4-165">![Kernel nel notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernel nel notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="b2ec4-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="b2ec4-166">b.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-166">b.</span></span> <span data-ttu-id="b2ec4-167">Eseguire hello seguente frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="b2ec4-168">Se è possibile recuperare correttamente l'output di hello, viene verificato il cluster HDInsight toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="b2ec4-169">Se si desidera tooupdate hello notebook configurazione tooconnect tooa diverso del cluster, aggiornare config. JSON hello con nuovo set di hello di valori, come illustrato nel passaggio 3 precedente.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="b2ec4-170">Perché installare Jupyter nel computer locale</span><span class="sxs-lookup"><span data-stu-id="b2ec4-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="b2ec4-171">Può essere un numero di motivi per cui si tooinstall Jupyter nel computer in uso e quindi connetterlo del cluster tooa Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="b2ec4-172">Anche se Jupyter notebook sono già disponibili nel cluster di hello Spark in HDInsight di Azure, installare Jupyter computer fornisce hello toocreate opzione notebook localmente, testare l'applicazione rispetto a un cluster in esecuzione e quindi caricare hello cluster toohello notebook.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="b2ec4-173">cluster di toohello notebook hello tooupload, è possibile caricare tali utilizzando server Jupyter notebook hello che è in esecuzione o hello cluster oppure salvarle toohello /HdiNotebooks cartella nell'account di archiviazione hello associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="b2ec4-174">Per ulteriori informazioni sulla modalità di archiviazione in cluster hello notebook, vedere [in cui sono archiviati i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="b2ec4-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="b2ec4-175">Con notebook hello disponibili in locale, è possibile connettere il cluster di Spark toodifferent in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="b2ec4-176">È possibile usare GitHub tooimplement un sistema di controllo del codice sorgente e controllo della versione per notebook hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="b2ec4-177">È inoltre possibile impostare un ambiente di collaborazione in cui più utenti lavorino con hello stesso blocco note.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="b2ec4-178">È possibile lavorare con i notebook in locale anche senza avere un cluster.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="b2ec4-179">È sufficiente un tootest cluster i blocchi appunti di base, non toomanually gestire i blocchi appunti o un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="b2ec4-180">Può essere tooconfigure più semplice ambiente di sviluppo locale che non l'installazione di server Jupyter tooconfigure hello in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="b2ec4-181">È possibile sfruttare tutti i software hello installato localmente senza configurare uno o più cluster remoto.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="b2ec4-182">Con Jupyter installato nel computer locale, più utenti possono eseguire hello stesso blocco appunti sul cluster Spark stesso in hello hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="b2ec4-183">In questo caso, vengono create più sessioni di Livy.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="b2ec4-184">Se si verifica un problema e si desidera che sarà tootrack un'attività complessa la sessione di inserire il cui appartiene l'utente toowhich toodebug.</span><span class="sxs-lookup"><span data-stu-id="b2ec4-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="b2ec4-185"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b2ec4-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b2ec4-186">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b2ec4-187">Scenari</span><span class="sxs-lookup"><span data-stu-id="b2ec4-187">Scenarios</span></span>
* [<span data-ttu-id="b2ec4-188">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b2ec4-189">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="b2ec4-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b2ec4-190">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="b2ec4-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b2ec4-191">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b2ec4-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b2ec4-192">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b2ec4-193">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="b2ec4-193">Create and run applications</span></span>
* [<span data-ttu-id="b2ec4-194">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="b2ec4-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b2ec4-195">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="b2ec4-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b2ec4-196">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="b2ec4-196">Tools and extensions</span></span>
* [<span data-ttu-id="b2ec4-197">Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="b2ec4-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b2ec4-198">Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota</span><span class="sxs-lookup"><span data-stu-id="b2ec4-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b2ec4-199">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b2ec4-200">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b2ec4-201">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="b2ec4-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="b2ec4-202">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="b2ec4-202">Manage resources</span></span>
* [<span data-ttu-id="b2ec4-203">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="b2ec4-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b2ec4-204">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2ec4-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
