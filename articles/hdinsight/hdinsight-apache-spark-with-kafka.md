---
title: 'Streaming Apache Spark con Kafka: Azure HDInsight | Microsoft Docs'
description: "Informazioni su come è possibile usare Apache Spark per trasmettere dati in streaming all'interno o all'esterno di Apache Kafka per mezzo di DStreams. In questo esempio i dati vengono trasmessi in streaming tramite un notebook Jupyter da Spark in HDInsight."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="05121-105">Esempio dello streaming Apache Spark (DStream) con Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="05121-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="05121-106">Informazioni su come è possibile usare Apache Spark per trasmettere dati in streaming all'interno o all'esterno di Apache Kafka su HDInsight per mezzo di DStreams.</span><span class="sxs-lookup"><span data-stu-id="05121-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="05121-107">Questo esempio usa un server Jupyter notebook che viene eseguito nel cluster di Spark.</span><span class="sxs-lookup"><span data-stu-id="05121-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="05121-108">La procedura descritta in questo documento permette di creare un gruppo di risorse di Azure che contiene sia un cluster Spark in HDInsight che un cluster Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05121-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="05121-109">Entrambi questi cluster si trovano all'interno di una rete virtuale di Azure, che consente al cluster Spark di comunicare direttamente con il cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="05121-110">Al termine della procedura descritta in questo documento, eliminare i cluster per evitare costi supplementari.</span><span class="sxs-lookup"><span data-stu-id="05121-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="05121-111">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="05121-111">Create the clusters</span></span>

<span data-ttu-id="05121-112">Apache Kafka in HDInsight non fornisce l'accesso ai broker Kafka tramite Internet pubblico.</span><span class="sxs-lookup"><span data-stu-id="05121-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="05121-113">Tutto ciò che comunica con Kafka deve trovarsi nella stessa rete virtuale di Azure dei nodi del cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="05121-114">Per questo esempio, i cluster Spark e Kafka si trovano entrambi in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05121-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="05121-115">Il diagramma seguente illustra il flusso delle comunicazioni tra i cluster:</span><span class="sxs-lookup"><span data-stu-id="05121-115">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramma dei cluster Spark e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="05121-117">Anche se Kafka è limitato alle comunicazioni all'interno della rete virtuale, è possibile accedere ad altri servizi del cluster tramite Internet, ad esempio SSH e Ambari.</span><span class="sxs-lookup"><span data-stu-id="05121-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="05121-118">Per altre informazioni sulle porte pubbliche disponibili con HDInsight, vedere [Porte e URI usati da HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="05121-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="05121-119">Anche se è possibile creare manualmente cluster Spark e Kafka e una rete virtuale di Azure, è più semplice usare un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05121-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="05121-120">Seguire questa procedura per distribuire cluster Spark e Kafka e una rete virtuale di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="05121-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="05121-121">Usare il pulsante seguente per accedere ad Azure e aprire il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05121-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="05121-122">Il modello di Azure Resource Manager è disponibile all'indirizzo **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="05121-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="05121-123">Per garantire la disponibilità di Kafka in HDInsight, il cluster deve contenere almeno tre nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="05121-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="05121-124">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="05121-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="05121-125">Questo modello crea un cluster HDInsight 3.6 sia per Kafka che per Spark.</span><span class="sxs-lookup"><span data-stu-id="05121-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="05121-126">Usare le informazioni seguenti per popolare le voci nel pannello **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="05121-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="05121-128">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="05121-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="05121-129">Questo gruppo contiene il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05121-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="05121-130">**Località**: scegliere una località geograficamente vicina.</span><span class="sxs-lookup"><span data-stu-id="05121-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="05121-131">**Base Cluster Name** (Nome di base del cluster): questo valore viene usato come nome di base per i cluster Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="05121-132">Ad esempio, se si immette **hdi** viene creato un cluster Spark denominato spark-hdi e un cluster Kafka denominato **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="05121-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="05121-133">**Cluster Login User Name** (Nome utente di accesso del cluster): nome utente amministratore per i cluster Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05121-134">**Cluster Login Password** (Password di accesso del cluster): password amministratore per i cluster Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05121-135">**SSH User Name** (Nome utente SSH): utente SSH da creare per i cluster Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05121-136">**SSH Password** (Password SSH): password dell'utente SSH per i cluster Spark e Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="05121-137">Leggere le **Condizioni** e quindi selezionare **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="05121-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="05121-138">Selezionare infine **Aggiungi al dashboard** e quindi **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="05121-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="05121-139">La creazione dei cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="05121-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="05121-140">Dopo aver creato le risorse, si viene reindirizzati a un pannello del gruppo di risorse che contiene i cluster e il dashboard Web.</span><span class="sxs-lookup"><span data-stu-id="05121-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Pannello Gruppo di risorse per la rete virtuale e i cluster](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="05121-142">Si noti che i nomi dei cluster HDInsight sono **spark-BASENAME** e **kafka-BASENAME**, dove BASENAME è il nome specificato per il modello.</span><span class="sxs-lookup"><span data-stu-id="05121-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="05121-143">Questi nomi verranno usati nei passaggi successivi per la connessione ai cluster.</span><span class="sxs-lookup"><span data-stu-id="05121-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="05121-144">Usare i notebook</span><span class="sxs-lookup"><span data-stu-id="05121-144">Use the notebooks</span></span>

<span data-ttu-id="05121-145">Il codice per l'esempio illustrato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="05121-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="05121-146">Seguire i passaggi nel file `README.md` per completare questo esempio.</span><span class="sxs-lookup"><span data-stu-id="05121-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="05121-147">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="05121-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="05121-148">Le procedure illustrate in questo documento creano entrambi i cluster nello stesso gruppo di risorse di Azure. È quindi possibile eliminare il gruppo di risorse dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05121-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="05121-149">In questo modo vengono rimosse tutte le risorse create seguendo le istruzioni di questo documento, la rete virtuale di Azure e l'account di archiviazione usato dai cluster.</span><span class="sxs-lookup"><span data-stu-id="05121-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05121-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05121-150">Next steps</span></span>

<span data-ttu-id="05121-151">Questo esempio ha illustrato l'uso di Spark per leggere e scrivere in Kafka.</span><span class="sxs-lookup"><span data-stu-id="05121-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="05121-152">Per trovare altri modi per lavorare con Kafka, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="05121-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="05121-153">Introduzione ad Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="05121-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="05121-154">Usare MirrorMaker per creare una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="05121-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="05121-155">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="05121-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

