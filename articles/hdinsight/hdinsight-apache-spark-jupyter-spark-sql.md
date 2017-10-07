---
title: cluster aaaCreate un Apache Spark in HDInsight di Azure | Documenti Microsoft
description: "Guida introduttiva di HDInsight Spark in modalità di cluster toocreate un Apache Spark in HDInsight."
keywords: guida introduttiva spark,spark interattivo,query interattiva,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="c4e5a-104">Creare un cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4e5a-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="c4e5a-105">In questo articolo viene illustrato come cluster di toocreate un Apache Spark in HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="c4e5a-106">Per informazioni su Spark in HDInsight, vedere [Panoramica: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="c4e5a-107">![Guida introduttiva diagramma che descrive i passaggi toocreate un cluster Apache Spark in Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "delle Guide rapide Spark usando Apache Spark in HDInsight. Passaggi illustrati: creare un cluster; eseguire una query interattiva Spark")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e5a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c4e5a-108">Prerequisites</span></span>

* <span data-ttu-id="c4e5a-109">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-109">**An Azure subscription**.</span></span> <span data-ttu-id="c4e5a-110">Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="c4e5a-111">Vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="c4e5a-112">Creare un cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c4e5a-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="c4e5a-113">In questa sezione viene creato un cluster HDInsight Spark usando un [modello di Azure Resource Manager](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="c4e5a-114">Per altri metodi di creazione dei cluster, vedere [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="c4e5a-115">Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="c4e5a-116">Immettere i seguenti valori hello:</span><span class="sxs-lookup"><span data-stu-id="c4e5a-116">Enter hello following values:</span></span>

    <span data-ttu-id="c4e5a-117">![Creare un cluster HDInsight Spark usando un modello di Azure Resource Manager](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Creare un cluster Spark in HDInsight usando un modello di Azure Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="c4e5a-118">**Sottoscrizione**: selezionare la sottoscrizione di Azure per questo cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="c4e5a-119">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="c4e5a-120">Gruppo di risorse viene utilizzato toomanage risorse di Azure per i progetti.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="c4e5a-121">**Percorso**: selezionare un percorso per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="c4e5a-122">modello Hello questo percorso viene utilizzato per la creazione di cluster hello anche come spazio di archiviazione cluster hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="c4e5a-123">**ClusterName**: immettere un nome per il cluster HDInsight hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="c4e5a-124">**Versione di Spark**: selezionare **2.0** come versione di hello che si desidera tooinstall nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="c4e5a-125">**Nome account di accesso e la password del cluster**: nome di account di accesso predefinito di hello è amministratore.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="c4e5a-126">**Nome utente e password SSH**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="c4e5a-127">Annotare questi valori</span><span class="sxs-lookup"><span data-stu-id="c4e5a-127">Write down these values.</span></span>  <span data-ttu-id="c4e5a-128">È necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="c4e5a-129">Selezionare **accetto le condizioni indicate in precedenza toohello**selezionare **Pin toodashboard**, quindi fare clic su **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="c4e5a-130">È possibile visualizzare un nuovo riquadro denominato Invio della distribuzione per Distribuzione modello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="c4e5a-131">Accetta cluster hello toocreate di circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="c4e5a-132">Se verifica un problema con la creazione di cluster HDInsight, è possibile che non si dispone hello delle corrette autorizzazioni toodo così.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="c4e5a-133">Per altre informazioni, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="c4e5a-134">In questo articolo viene creato un cluster Spark che usa [archiviazione BLOB di archiviazione di Azure come hello del cluster](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="c4e5a-135">È inoltre possibile creare un cluster Spark che usa [archivio Azure Data Lake](hdinsight-hadoop-use-data-lake-store.md) come spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="c4e5a-136">Per istruzioni, vedere [Creare un cluster HDInsight con Archivio Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="c4e5a-137">Eseguire una query Hive usando Spark SQL</span><span class="sxs-lookup"><span data-stu-id="c4e5a-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="c4e5a-138">Quando si utilizza un server Jupyter notebook configurato per il cluster HDInsight Spark, si ottiene un set di impostazioni `sqlContext` che è possibile utilizzare le query Hive toorun utilizzando Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="c4e5a-139">In questa sezione viene illustrato come un server Jupyter notebook toostart e quindi eseguire una query Hive base.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="c4e5a-140">Aprire hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="c4e5a-141">Se si è scelto di dashboard di toohello toopin hello del cluster, fare clic su riquadro cluster hello dal Pannello di hello dashboard toolaunch hello cluster.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="c4e5a-142">Se si non blocca hello cluster toohello dashboard nel riquadro di sinistra hello, fare clic su **cluster HDInsight**, quindi fare clic su cluster hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="c4e5a-143">In **Collegamenti rapidi** fare clic su **Dashboard cluster** e quindi su **Notebook di Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="c4e5a-144">Se richiesto, immettere le credenziali di amministratore hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="c4e5a-145">![Aprire Server Jupyter notebook toorun Spark SQL query interattivo](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "aprire Jupyter notebook toorun interattivo Spark nella query SQL")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4e5a-146">È inoltre possibile accedere notebook Jupyter hello per il cluster usando hello apertura URL seguente nel browser.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c4e5a-147">Sostituire **CLUSTERNAME** con nome hello del cluster:</span><span class="sxs-lookup"><span data-stu-id="c4e5a-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="c4e5a-148">Creare un notebook.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-148">Create a notebook.</span></span> <span data-ttu-id="c4e5a-149">Fare clic su **Nuovo** e quindi su **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="c4e5a-150">![Creare una query di Spark SQL interattiva Jupyter notebook toorun](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "creare una query di Spark SQL interattiva Jupyter notebook toorun")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="c4e5a-151">Un nuovo blocco appunti viene creato e aperto con il nome di hello Untitled(Untitled.pynb).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="c4e5a-152">Fare clic sul nome di blocco per Appunti hello nella parte superiore di hello e immettere un nome descrittivo, se si desidera.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="c4e5a-153">![Specificare un nome per hello Jupter notebook toorun Spark query interattivo da](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "specificare un nome per hello Jupter notebook toorun Spark query interattivo da")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="c4e5a-154">Esempio hello Incolla del codice in una cella vuota e quindi premere **MAIUSC + INVIO** codice hello toorun.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="c4e5a-155">Nel seguente codice hello `%%sql` (magic sql denominato hello) indica hello toouse di Jupyter notebook preimpostato `sqlContext` query Hive di hello toorun.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="c4e5a-156">query Hello recupera hello prime 10 righe da una tabella Hive (**hivesampletable**) che è disponibile per impostazione predefinita in tutti i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="c4e5a-157">![Query Hive in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Query Hive in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="c4e5a-158">Per ulteriori informazioni su hello `%%sql` magic e hello predefinito contesti, vedere [Jupyter kernel disponibile per un cluster HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="c4e5a-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4e5a-159">Ogni volta che si esegue una query in Jupyter, il titolo della finestra del browser web viene illustrato un **(occupata)** stato insieme a titolo di hello notebook.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="c4e5a-160">Viene visualizzato anche un toohello Avanti cerchio pieno **PySpark** testo nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="c4e5a-161">Dopo aver completato il processo di hello, assume la forma cerchio tooa.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="c4e5a-162">schermata Ciao necessario aggiornare l'output della query tooshow hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="c4e5a-163">![Output della query Hive in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Output della query Hive in HDInsight Spark")</span><span class="sxs-lookup"><span data-stu-id="c4e5a-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="c4e5a-164">Arresto delle risorse cluster di hello notebook toorelease hello al termine dell'esecuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="c4e5a-165">toodo in questo caso, da hello **File** menu notebook hello, fare clic su **chiudere e interrompere**.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="c4e5a-166">Se si prevede i passaggi successivi di toocomplete hello in un secondo momento, assicurarsi che eliminare il cluster di HDInsight hello che è stato creato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="c4e5a-167">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="c4e5a-167">Next step</span></span> 

<span data-ttu-id="c4e5a-168">In questo articolo si è appreso come cluster di toocreate un HDInsight Spark ed eseguire una base di Spark SQL eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="c4e5a-169">Spostare toohello Avanti articolo toolearn come toouse un HDInsight Spark cluster toorun interattivo query su dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="c4e5a-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c4e5a-170">Eseguire query interattive in un cluster di Azure HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c4e5a-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



