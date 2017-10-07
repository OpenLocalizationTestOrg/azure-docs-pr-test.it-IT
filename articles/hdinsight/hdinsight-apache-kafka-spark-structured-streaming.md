---
title: aaaApache Spark Streaming strutturati con Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come Apache Spark streaming (DStream) tooget dati in o da Apache Kafka toouse. In questo esempio i dati vengono trasmessi in streaming tramite un notebook Jupyter da Spark in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="894f3-104">Usare lo streaming strutturato Spark con Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="894f3-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="894f3-105">Informazioni su come toouse Spark strutturati Streaming dati tooread Kafka Apache in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="894f3-105">Learn how toouse Spark Structured Streaming tooread data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="894f3-106">Lo streaming strutturato Spark è un motore di elaborazione del flusso basato su Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="894f3-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="894f3-107">Consente di calcoli di streaming tooexpress hello stesso come il calcolo di batch in dati statici.</span><span class="sxs-lookup"><span data-stu-id="894f3-107">It allows you tooexpress streaming computations hello same as batch computation on static data.</span></span> <span data-ttu-id="894f3-108">Per ulteriori informazioni sui flussi strutturati, vedere hello [strutturati Streaming Guida per programmatori [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) in Apache.org.</span><span class="sxs-lookup"><span data-stu-id="894f3-108">For more information on Structured Streaming, see hello [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="894f3-109">In questo esempio viene usato Spark 2.1 in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="894f3-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="894f3-110">Lo streaming strutturato è considerato __alfa__ in Spark 2.1.</span><span class="sxs-lookup"><span data-stu-id="894f3-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="894f3-111">procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia un Spark in HDInsight e un Kafka nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="894f3-111">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="894f3-112">Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Spark comunicare hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="894f3-112">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="894f3-113">Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.</span><span class="sxs-lookup"><span data-stu-id="894f3-113">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="894f3-114">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="894f3-114">Create hello clusters</span></span>

<span data-ttu-id="894f3-115">Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="894f3-115">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="894f3-116">Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="894f3-116">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="894f3-117">In questo esempio hello Kafka sia cluster Spark si trovano in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="894f3-117">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="894f3-118">Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:</span><span class="sxs-lookup"><span data-stu-id="894f3-118">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramma dei cluster Spark e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="894f3-120">servizio Kafka Hello è limitato toocommunication all'interno di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-120">hello Kafka service is limited toocommunication within hello virtual network.</span></span> <span data-ttu-id="894f3-121">Altri servizi in cluster hello, ad esempio SSH e Ambari, accessibile tramite internet hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-121">Other services on hello cluster, such as SSH and Ambari, can be accessed over hello internet.</span></span> <span data-ttu-id="894f3-122">Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="894f3-122">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="894f3-123">È possibile creare una rete virtuale di Azure, Kafka e Spark cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="894f3-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="894f3-124">Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Spark cluster tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="894f3-124">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="894f3-125">Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-125">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="894f3-126">Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span><span class="sxs-lookup"><span data-stu-id="894f3-126">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="894f3-127">Questo modello consente di creare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="894f3-127">This template creates hello following resources:</span></span>

    * <span data-ttu-id="894f3-128">Kafka nel cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="894f3-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="894f3-129">Spark nel cluster HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="894f3-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="894f3-130">Una rete virtuale di Azure che contiene il cluster di HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-130">An Azure Virtual Network, which contains hello HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="894f3-131">Hello strutturati streaming blocco appunti utilizzato in questo esempio richiede Spark in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="894f3-131">hello structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="894f3-132">Se si utilizza una versione precedente di Spark in HDInsight, si ricevono errori quando si utilizza notebook hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-132">If you use an earlier version of Spark on HDInsight, you receive errors when using hello notebook.</span></span>

2. <span data-ttu-id="894f3-133">Hello utilizzare seguendo le voci di informazioni toopopulate hello hello **distribuzione personalizzata** pannello:</span><span class="sxs-lookup"><span data-stu-id="894f3-133">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="894f3-135">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="894f3-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="894f3-136">Questo gruppo contiene cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-136">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="894f3-137">**Percorso**: selezionare un tooyou geograficamente Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="894f3-137">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="894f3-138">**Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Spark e Kafka hello hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-138">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="894f3-139">Ad esempio, se si immette **hdi** viene creato un cluster Spark denominato spark-hdi e un cluster Kafka denominato **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="894f3-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="894f3-140">**Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-140">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="894f3-141">**Password di account di accesso cluster**: password dell'utente per i cluster Spark e Kafka hello hello admin.</span><span class="sxs-lookup"><span data-stu-id="894f3-141">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="894f3-142">**Nome utente SSH**: hello toocreate utente SSH per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-142">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="894f3-143">**Password SSH**: password hello per utente SSH hello per i cluster Spark e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-143">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="894f3-144">Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.</span><span class="sxs-lookup"><span data-stu-id="894f3-144">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="894f3-145">Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="894f3-145">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="894f3-146">Sono necessari circa 20 minuti toocreate cluster hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-146">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="894f3-147">Dopo avere create le risorse di hello, verrà reindirizzato toohello pannello gruppo della risorsa.</span><span class="sxs-lookup"><span data-stu-id="894f3-147">Once hello resources have been created, you are redirected toohello resource group blade.</span></span>

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="894f3-149">Si noti che sono nomi hello dei cluster HDInsight hello **spark BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato.</span><span class="sxs-lookup"><span data-stu-id="894f3-149">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="894f3-150">Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="894f3-150">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="get-hello-kafka-brokers"></a><span data-ttu-id="894f3-151">Ottenere hello Kafka Broker</span><span class="sxs-lookup"><span data-stu-id="894f3-151">Get hello Kafka brokers</span></span>

<span data-ttu-id="894f3-152">codice in questo esempio Hello connette toohello Kafka gli host in cluster Kafka hello di Service broker.</span><span class="sxs-lookup"><span data-stu-id="894f3-152">hello code in this example connects toohello Kafka broker hosts in hello Kafka cluster.</span></span> <span data-ttu-id="894f3-153">toofind hello host di Service broker Kafka, usare hello esempio PowerShell o Bash seguente:</span><span class="sxs-lookup"><span data-stu-id="894f3-153">toofind hello Kafka broker hosts, use hello following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="894f3-154">In questo esempio prevede `$PASSWORD` password hello toocontain per account di accesso cluster hello e `$CLUSTERNAME` nome hello toocontain di hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="894f3-154">This example expects `$PASSWORD` toocontain hello password for hello cluster login, and `$CLUSTERNAME` toocontain hello name of hello Kafka cluster.</span></span>
>
> <span data-ttu-id="894f3-155">Questo esempio viene utilizzato hello [jq](https://stedolan.github.io/jq/) dati tooparse utilità fuori documento JSON hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-155">This example uses hello [jq](https://stedolan.github.io/jq/) utility tooparse data out of hello JSON document.</span></span>

<span data-ttu-id="894f3-156">Hello l'output è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="894f3-156">hello output is similar toohello following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="894f3-157">Salvare queste informazioni, viene utilizzato in hello le sezioni seguenti di questo documento.</span><span class="sxs-lookup"><span data-stu-id="894f3-157">Save this information, as it is used in hello following sections of this document.</span></span>

## <a name="get-hello-notebooks"></a><span data-ttu-id="894f3-158">Ottenere notebook hello</span><span class="sxs-lookup"><span data-stu-id="894f3-158">Get hello notebooks</span></span>

<span data-ttu-id="894f3-159">codice Hello ad esempio hello descritta in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span><span class="sxs-lookup"><span data-stu-id="894f3-159">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-hello-notebooks"></a><span data-ttu-id="894f3-160">Caricare i notebook hello</span><span class="sxs-lookup"><span data-stu-id="894f3-160">Upload hello notebooks</span></span>

<span data-ttu-id="894f3-161">Utilizzare hello seguenti passaggi viene notebook hello tooupload da tooyour progetto hello Spark nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="894f3-161">Use hello following steps tooupload hello notebooks from hello project tooyour Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="894f3-162">Nel web browser, connettersi toohello server Jupyter notebook nel cluster di Spark.</span><span class="sxs-lookup"><span data-stu-id="894f3-162">In your web browser, connect toohello Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="894f3-163">In hello seguente URL, sostituire `CLUSTERNAME` con nome hello del cluster Kafka:</span><span class="sxs-lookup"><span data-stu-id="894f3-163">In hello following URL, replace `CLUSTERNAME` with hello name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="894f3-164">Quando richiesto, immettere l'account di accesso cluster hello (amministrazione) e la password utilizzata per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="894f3-164">When prompted, enter hello cluster login (admin) and password used when you created hello cluster.</span></span>

2. <span data-ttu-id="894f3-165">Da hello parte superiore destra della pagina hello, utilizzare hello __caricare__ hello tooupload pulsante __flusso-Tweets-To_Kafka.ipynb__ cluster toohello di file.</span><span class="sxs-lookup"><span data-stu-id="894f3-165">From hello upper right side of hello page, use hello __Upload__ button tooupload hello __Stream-Tweets-To_Kafka.ipynb__ file toohello cluster.</span></span> <span data-ttu-id="894f3-166">Selezionare __aprire__ caricamento hello toostart.</span><span class="sxs-lookup"><span data-stu-id="894f3-166">Select __Open__ toostart hello upload.</span></span>

    ![Utilizzare hello caricamento pulsante tooselect e caricare un blocco per Appunti](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selezionare file KafkaStreaming.ipynb hello](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="894f3-169">Trovare hello __flusso-Tweets-To_Kafka.ipynb__ voce nell'elenco di hello di blocchi appunti e selezionare __caricare__ pulsante accanto a esso.</span><span class="sxs-lookup"><span data-stu-id="894f3-169">Find hello __Stream-Tweets-To_Kafka.ipynb__ entry in hello list of notebooks, and select __Upload__ button beside it.</span></span>

    ![Caricamento di hello utilizzare accanto a tooupload di voce KafkaStreaming.ipynb hello è server notebook toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="894f3-171">Ripetere i passaggi da 1 a 3 hello di tooload __Spark-struttura-Streaming-da-Kafka.ipynb__ notebook.</span><span class="sxs-lookup"><span data-stu-id="894f3-171">Repeat steps 1-3 tooload hello __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="894f3-172">Caricamento di tweet in Kafka</span><span class="sxs-lookup"><span data-stu-id="894f3-172">Load tweets into Kafka</span></span>

<span data-ttu-id="894f3-173">Una volta caricati i file hello, selezionare hello __flusso-Tweets-To_Kafka.ipynb__ notebook hello tooopen di voce.</span><span class="sxs-lookup"><span data-stu-id="894f3-173">Once hello files have been uploaded, select hello __Stream-Tweets-To_Kafka.ipynb__ entry tooopen hello notebook.</span></span> <span data-ttu-id="894f3-174">Seguire i passaggi hello hello notebook tooload tweets in Kafka.</span><span class="sxs-lookup"><span data-stu-id="894f3-174">Follow hello steps in hello notebook tooload tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="894f3-175">Elaborazione dei tweet con lo streaming strutturato Spark</span><span class="sxs-lookup"><span data-stu-id="894f3-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="894f3-176">Home page di server Jupyter Notebook hello, selezionare hello __Spark-struttura-Streaming-da-Kafka.ipynb__ voce.</span><span class="sxs-lookup"><span data-stu-id="894f3-176">From hello Jupyter Notebook home page, select hello __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="894f3-177">Seguire i passaggi hello hello notebook tooload TWEET da Kafka tramite flusso strutturati Spark.</span><span class="sxs-lookup"><span data-stu-id="894f3-177">Follow hello steps in hello notebook tooload tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="894f3-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="894f3-178">Next steps</span></span>

<span data-ttu-id="894f3-179">Ora che si è appreso come toouse Spark strutturata di flusso, vedere hello seguenti documenti toolearn ulteriori informazioni sull'utilizzo di Spark e Kafka:</span><span class="sxs-lookup"><span data-stu-id="894f3-179">Now that you have learned how toouse Spark Structured Streaming, see hello following documents toolearn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="894f3-180">[La modalità di nascita streaming (DStream) con Kafka toouse](hdinsight-apache-spark-with-kafka.md).</span><span class="sxs-lookup"><span data-stu-id="894f3-180">[How toouse Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="894f3-181">Iniziare a usare un notebook Jupyter e Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="894f3-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)