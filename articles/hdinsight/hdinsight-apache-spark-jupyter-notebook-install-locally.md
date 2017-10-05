---
title: Installare Jupyter localmente e connetterlo a un cluster Azure HDInsight Spark | Microsoft Docs
description: Informazioni su come installare il notebook di Jupyter in locale nel computer e su come connetterlo a un cluster Apache Spark in Azure HDInsight.
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="72388-103">Installare un notebook di Jupyter in locale e connetterlo ad Apache Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="72388-104">Questo articolo illustra come installare Jupyter Notebook, insieme ai kernel personalizzati PySpark (per Python) e Spark (per Scala) e al magic Spark, e come connettere l'applicazione a un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72388-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="72388-105">L'installazione di Jupyter nel computer locale può essere dettata da molti motivi e può anche presentare alcuni problemi.</span><span class="sxs-lookup"><span data-stu-id="72388-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="72388-106">Per altre informazioni, vedere la sezione [Perché installare Jupyter nel computer locale](#why-should-i-install-jupyter-on-my-computer) alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="72388-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="72388-107">L'installazione di Jupyter e del magic Spark nel computer si articola in tre passaggi chiave.</span><span class="sxs-lookup"><span data-stu-id="72388-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="72388-108">Installare Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="72388-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="72388-109">Installare i kernel PySpark e Spark con il magic Spark</span><span class="sxs-lookup"><span data-stu-id="72388-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="72388-110">Configurare il magic Spark per l'accesso al cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="72388-111">Per altre informazioni sui kernel personalizzati e su Spark magic disponibili per Jupyter Notebook con il cluster HDInsight, vedere [Kernel disponibili per Jupyter Notebook con cluster HDInsight Spark Linux su HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="72388-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72388-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72388-112">Prerequisites</span></span>
<span data-ttu-id="72388-113">I prerequisiti elencati di seguito non riguardano l'installazione di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="72388-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="72388-114">Riguardano invece la connessione di Jupyter Notebook a un cluster HDInsight dopo l'installazione.</span><span class="sxs-lookup"><span data-stu-id="72388-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="72388-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="72388-115">An Azure subscription.</span></span> <span data-ttu-id="72388-116">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="72388-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="72388-117">Un cluster Apache Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72388-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="72388-118">Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="72388-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="72388-119">Installare Jupyter Notebook nel computer</span><span class="sxs-lookup"><span data-stu-id="72388-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="72388-120">Prima di installare i notebook Jupyter è necessario installare Python.</span><span class="sxs-lookup"><span data-stu-id="72388-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="72388-121">Sia Python che Jupyter sono disponibili come parte della [distribuzione Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="72388-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="72388-122">Quando si installa Anaconda, viene installata una distribuzione di Python.</span><span class="sxs-lookup"><span data-stu-id="72388-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="72388-123">Dopo aver installato Anaconda, aggiungere l'installazione di Jupyter mediante l'esecuzione dei comandi appropriati.</span><span class="sxs-lookup"><span data-stu-id="72388-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="72388-124">Scaricare il [programma di installazione di Anaconda](https://www.continuum.io/downloads) per la piattaforma in uso ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="72388-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="72388-125">Quando si esegue l'installazione guidata, assicurarsi di selezionare l'opzione per l'aggiunta di Anaconda alla variabile PATH.</span><span class="sxs-lookup"><span data-stu-id="72388-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="72388-126">Eseguire il comando seguente per installare Jupyter.</span><span class="sxs-lookup"><span data-stu-id="72388-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="72388-127">Per altre informazioni sull'installazione di Jupyter, vedere l'argomento relativo all' [installazione di Jupyter mediante Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span><span class="sxs-lookup"><span data-stu-id="72388-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="72388-128">Installare i kernel e il magic Spark</span><span class="sxs-lookup"><span data-stu-id="72388-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="72388-129">Per le istruzioni su come installare il magic Spark, i kernel Spark e PySpark, seguire le istruzioni di installazione nella [documentazione sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="72388-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="72388-130">Il primo passaggio nella documentazione relativa al magic Spark richiede di installarlo.</span><span class="sxs-lookup"><span data-stu-id="72388-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="72388-131">Sostituire il primo passaggio nel collegamento con i comandi seguenti, a seconda della versione del cluster HDInsight a cui ci si connetterà.</span><span class="sxs-lookup"><span data-stu-id="72388-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="72388-132">Seguire quindi i passaggi rimanenti nella documentazione relativa al magic Spark.</span><span class="sxs-lookup"><span data-stu-id="72388-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="72388-133">Se si intende installare i diversi kernel, è necessario eseguire il passaggio 3 nella sezione delle istruzioni di installazione del magic Spark.</span><span class="sxs-lookup"><span data-stu-id="72388-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="72388-134">Per i cluster v3.4, installare sparkmagic 0.2.3 eseguendo `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="72388-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="72388-135">Per i cluster v3.5 e v3.6, installare sparkmagic 0.11.2 eseguendo `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="72388-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="72388-136">Configurare il magic Spark per la connessione al cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="72388-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="72388-137">Questa sezione illustra come configurare il magic Spark installato in precedenza per la connessone a un cluster Apache Spark. È necessario che tale cluster sia già stato creato in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72388-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="72388-138">Le informazioni di configurazione di Jupyter sono in genere archiviate nella home directory dell'utente.</span><span class="sxs-lookup"><span data-stu-id="72388-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="72388-139">Per individuare la home directory su una qualsiasi piattaforma del sistema operativo, digitare i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="72388-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="72388-140">Avviare la shell di Python.</span><span class="sxs-lookup"><span data-stu-id="72388-140">Start the Python shell.</span></span> <span data-ttu-id="72388-141">In una finestra di comando digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="72388-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="72388-142">Nella shell di Python immettere il comando seguente per individuare la home directory.</span><span class="sxs-lookup"><span data-stu-id="72388-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="72388-143">Passare alla home directory e, se non esiste già, creare una cartella denominata **.sparkmagic** .</span><span class="sxs-lookup"><span data-stu-id="72388-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="72388-144">All'interno della cartella creare un file denominato **config.json** e aggiungere a quest'ultimo il frammento di codice JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="72388-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="72388-145">Sostituire **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="72388-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="72388-146">È possibile usare diverse utilità del linguaggio di programmazione preferito o uno strumento online per convertire la password corrente in una password con codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="72388-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="72388-147">Configurare le impostazioni di heartbeat corrette in `config.json`.</span><span class="sxs-lookup"><span data-stu-id="72388-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="72388-148">Queste impostazioni devono essere aggiunte allo stesso livello dei frammenti `kernel_python_credentials` e `kernel_scala_credentials` aggiunti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="72388-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="72388-149">Per un esempio di come e dove aggiungere le impostazioni di heartbeat, vedere questo [file config.json di esempio](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="72388-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="72388-150">Per `sparkmagic 0.2.3` (cluster v3.4), includere:</span><span class="sxs-lookup"><span data-stu-id="72388-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="72388-151">Per `sparkmagic 0.11.2` (cluster v3.5 e v3.6), includere:</span><span class="sxs-lookup"><span data-stu-id="72388-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="72388-152">Gli heartbeat vengono inviati per assicurare che le sessioni non vengano perse.</span><span class="sxs-lookup"><span data-stu-id="72388-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="72388-153">Quando un computer va in sospensione o viene arrestato, l'heartbeat non verrà inviato e la sessione verrà quindi eliminata.</span><span class="sxs-lookup"><span data-stu-id="72388-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="72388-154">Per disabilitare questo comportamento per i cluster v3.4, è possibile impostare la configurazione di Livy `livy.server.interactive.heartbeat.timeout` su `0` dall'interfaccia utente di Ambari.</span><span class="sxs-lookup"><span data-stu-id="72388-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="72388-155">Per i cluster v3.5, se non si imposta la configurazione 3.5 precedente, la sessione non verrà eliminata.</span><span class="sxs-lookup"><span data-stu-id="72388-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="72388-156">Avviare Jupyter.</span><span class="sxs-lookup"><span data-stu-id="72388-156">Start Jupyter.</span></span> <span data-ttu-id="72388-157">Usare il comando seguente dal prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="72388-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="72388-158">Verificare che sia possibile connettersi al cluster mediante Jupyter Notebook e usare il magic Spark disponibile con i kernel.</span><span class="sxs-lookup"><span data-stu-id="72388-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="72388-159">Eseguire i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="72388-159">Perform the following steps.</span></span>

    <span data-ttu-id="72388-160">a.</span><span class="sxs-lookup"><span data-stu-id="72388-160">a.</span></span> <span data-ttu-id="72388-161">Creare un nuovo notebook.</span><span class="sxs-lookup"><span data-stu-id="72388-161">Create a new notebook.</span></span> <span data-ttu-id="72388-162">Nell'angolo a destra fare clic su **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="72388-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="72388-163">Verranno visualizzati il kernel predefinito **Python2** e i due nuovi kernel installati, **PySpark** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="72388-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="72388-164">Fare clic su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="72388-164">Click **PySpark**.</span></span>

    <span data-ttu-id="72388-165">![Kernel nel notebook di Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernel nel notebook di Jupyter")</span><span class="sxs-lookup"><span data-stu-id="72388-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="72388-166">b.</span><span class="sxs-lookup"><span data-stu-id="72388-166">b.</span></span> <span data-ttu-id="72388-167">Eseguire il frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="72388-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="72388-168">Se è stato possibile recuperare l'output, viene verificata la connessione al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72388-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="72388-169">Se si desidera aggiornare la configurazione del notebook per connettersi a un cluster differente, aggiornare il file config.json con un nuovo set di valori come illustrato nel Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="72388-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="72388-170">Perché installare Jupyter nel computer locale</span><span class="sxs-lookup"><span data-stu-id="72388-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="72388-171">Può esistere una serie di motivi per cui è consigliabile installare Jupyter nel computer in uso e quindi connetterlo a un cluster Spark in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72388-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="72388-172">Anche se i notebook Jupyter sono già disponibili nel cluster Spark in Azure HDInsight, l'installazione di Jupyter nel computer offre la possibilità di creare i notebook in locale, testare l'applicazione con un cluster in esecuzione e quindi caricare i notebook nel cluster.</span><span class="sxs-lookup"><span data-stu-id="72388-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="72388-173">È possibile caricare i notebook nel cluster usando Jupyter Notebook già in esecuzione sul cluster oppure salvare i notebook nella cartella /HdiNotebooks nell'account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="72388-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="72388-174">Per altre informazioni sul modo in cui i notebook vengono archiviati nel cluster, vedere la sezione [Dove sono archiviati i notebook?](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)</span><span class="sxs-lookup"><span data-stu-id="72388-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="72388-175">Con i notebook disponibili in locale è possibile connettersi a cluster Spark diversi in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72388-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="72388-176">È possibile usare GitHub per implementare un sistema di controllo del codice sorgente e usare il controllo della versione per il notebook.</span><span class="sxs-lookup"><span data-stu-id="72388-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="72388-177">È anche possibile avere a disposizione un ambiente di collaborazione in cui più utenti possono lavorare allo stesso notebook.</span><span class="sxs-lookup"><span data-stu-id="72388-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="72388-178">È possibile lavorare con i notebook in locale anche senza avere un cluster.</span><span class="sxs-lookup"><span data-stu-id="72388-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="72388-179">È necessario avere un cluster solo per eseguire i test dei notebook, non per gestire manualmente i notebook o un ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="72388-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="72388-180">Può essere più semplice configurare il proprio ambiente di sviluppo locale che configurare l'installazione di Jupyter nel cluster.</span><span class="sxs-lookup"><span data-stu-id="72388-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="72388-181">È possibile sfruttare tutto il software installato localmente senza configurare uno o più cluster remoti.</span><span class="sxs-lookup"><span data-stu-id="72388-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="72388-182">Con Jupyter installato nel computer locale più utenti possono eseguire contemporaneamente lo stesso notebook nello stesso cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="72388-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="72388-183">In questo caso, vengono create più sessioni di Livy.</span><span class="sxs-lookup"><span data-stu-id="72388-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="72388-184">Se si verifica un problema e si vuole eseguire il debug, tenere traccia della sessione di Livy che appartiene l'utente sarà un'attività complessa.</span><span class="sxs-lookup"><span data-stu-id="72388-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="72388-185"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="72388-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="72388-186">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="72388-187">Scenari</span><span class="sxs-lookup"><span data-stu-id="72388-187">Scenarios</span></span>
* [<span data-ttu-id="72388-188">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="72388-189">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="72388-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="72388-190">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="72388-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="72388-191">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="72388-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="72388-192">Analisi dei log del sito Web mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="72388-193">Creare ed eseguire applicazioni</span><span class="sxs-lookup"><span data-stu-id="72388-193">Create and run applications</span></span>
* [<span data-ttu-id="72388-194">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="72388-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="72388-195">Eseguire processi in modalità remota in un cluster Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="72388-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="72388-196">Strumenti ed estensioni</span><span class="sxs-lookup"><span data-stu-id="72388-196">Tools and extensions</span></span>
* [<span data-ttu-id="72388-197">Usare il plug-in degli strumenti HDInsight per IntelliJ IDEA per creare e inviare applicazioni Spark Scala</span><span class="sxs-lookup"><span data-stu-id="72388-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="72388-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely (Usare il plug-in Strumenti HDInsight per IntelliJ IDEA per eseguire il debug di applicazioni Spark in remoto)</span><span class="sxs-lookup"><span data-stu-id="72388-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="72388-199">Usare i notebook di Zeppelin con un cluster Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="72388-200">Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="72388-201">Usare pacchetti esterni con i notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="72388-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="72388-202">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="72388-202">Manage resources</span></span>
* [<span data-ttu-id="72388-203">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="72388-204">Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="72388-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
