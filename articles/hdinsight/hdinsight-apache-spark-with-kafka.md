---
title: aaaApache Spark streaming con Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati di toostream Spark Apache Spark in o da Apache Kafka utilizzando DStreams toouse. In questo esempio i dati vengono trasmessi in streaming tramite un notebook Jupyter da Spark in HDInsight.
keywords: esempio kafka,kafka zookeeper,spark streaming kafka,esempio spark streaming kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="809c8-105">Esempio dello streaming Apache Spark (DStream) con Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="809c8-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="809c8-106">Informazioni su come dati di toostream Spark Apache Spark in o da Apache Kafka in HDInsight mediante DStreams toouse.</span><span class="sxs-lookup"><span data-stu-id="809c8-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="809c8-107">Questo esempio viene utilizzato un server Jupyter notebook esecuzione nel cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="809c8-108">procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia un Spark in HDInsight e un Kafka nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="809c8-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="809c8-109">Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Spark comunicare hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="809c8-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="809c8-110">Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.</span><span class="sxs-lookup"><span data-stu-id="809c8-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="809c8-111">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="809c8-111">Create hello clusters</span></span>

<span data-ttu-id="809c8-112">Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="809c8-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="809c8-113">Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="809c8-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="809c8-114">In questo esempio hello Kafka sia cluster Spark si trovano in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="809c8-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="809c8-115">Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:</span><span class="sxs-lookup"><span data-stu-id="809c8-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramma dei cluster Spark e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="809c8-117">Anche se Kafka stesso toocommunication limitato all'interno di rete virtuale hello, altri servizi in cluster hello, ad esempio possibile accedere tramite SSH e Ambari hello internet.</span><span class="sxs-lookup"><span data-stu-id="809c8-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="809c8-118">Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="809c8-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="809c8-119">È possibile creare una rete virtuale di Azure, Kafka e Spark cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="809c8-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="809c8-120">Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Spark cluster tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="809c8-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="809c8-121">Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="809c8-122">Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="809c8-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="809c8-123">disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="809c8-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="809c8-124">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="809c8-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="809c8-125">Questo modello crea un cluster HDInsight 3.6 sia per Kafka che per Spark.</span><span class="sxs-lookup"><span data-stu-id="809c8-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="809c8-126">Hello utilizzare seguendo le voci di informazioni toopopulate hello hello **distribuzione personalizzata** pannello:</span><span class="sxs-lookup"><span data-stu-id="809c8-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="809c8-128">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="809c8-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="809c8-129">Questo gruppo contiene cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="809c8-130">**Percorso**: selezionare un tooyou geograficamente Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="809c8-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="809c8-131">**Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Spark e Kafka hello hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="809c8-132">Ad esempio, se si immette **hdi** viene creato un cluster Spark denominato spark-hdi e un cluster Kafka denominato **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="809c8-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="809c8-133">**Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="809c8-134">**Password di account di accesso cluster**: password dell'utente per i cluster Spark e Kafka hello hello admin.</span><span class="sxs-lookup"><span data-stu-id="809c8-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="809c8-135">**Nome utente SSH**: hello toocreate utente SSH per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="809c8-136">**Password SSH**: password hello per utente SSH hello per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="809c8-137">Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.</span><span class="sxs-lookup"><span data-stu-id="809c8-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="809c8-138">Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="809c8-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="809c8-139">Sono necessari circa 20 minuti toocreate cluster hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="809c8-140">Dopo avere create le risorse di hello, verrà reindirizzato tooa pannello per gruppo di risorse hello che contiene i cluster hello e dashboard web.</span><span class="sxs-lookup"><span data-stu-id="809c8-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="809c8-142">Si noti che sono nomi hello dei cluster HDInsight hello **spark BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato.</span><span class="sxs-lookup"><span data-stu-id="809c8-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="809c8-143">Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="809c8-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="809c8-144">Utilizzare i blocchi appunti hello</span><span class="sxs-lookup"><span data-stu-id="809c8-144">Use hello notebooks</span></span>

<span data-ttu-id="809c8-145">codice Hello ad esempio hello descritta in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="809c8-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="809c8-146">Seguire i passaggi hello hello `README.md` file toocomplete in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="809c8-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="809c8-147">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="809c8-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="809c8-148">Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="809c8-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="809c8-149">Eliminazione gruppo hello rimuove tutte le risorse create eseguendo questo documento, hello rete virtuale di Azure e l'account di archiviazione utilizzato dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="809c8-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="809c8-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="809c8-150">Next steps</span></span>

<span data-ttu-id="809c8-151">In questo esempio è stato descritto come toouse nascita tooread e scrivere tooKafka.</span><span class="sxs-lookup"><span data-stu-id="809c8-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="809c8-152">Utilizzare hello seguendo i collegamenti toodiscover toowork altri modi con Kafka:</span><span class="sxs-lookup"><span data-stu-id="809c8-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="809c8-153">Introduzione ad Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="809c8-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="809c8-154">Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="809c8-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="809c8-155">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="809c8-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

