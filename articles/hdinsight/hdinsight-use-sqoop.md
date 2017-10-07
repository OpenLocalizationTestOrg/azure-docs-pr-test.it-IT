---
title: aaaRun Sqoop Apache processi con Azure HDInsight (Hadoop) | Documenti Microsoft
description: Informazioni su come toouse Azure PowerShell da un toorun workstation Sqoop importare ed esportare tra un cluster Hadoop e un database SQL di Azure.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="787aa-103">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="787aa-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="787aa-104">Informazioni su come toouse Sqoop in HDInsight tooimport ed Esporta tra cluster HDInsight e database SQL di Azure o database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787aa-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="787aa-105">Anche se Hadoop è una scelta naturale per l'elaborazione dei dati non strutturati e semistrutturati, ad esempio i registri e file, è inoltre possibile un necessità tooprocess strutturato i dati archiviati nei database relazionali.</span><span class="sxs-lookup"><span data-stu-id="787aa-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="787aa-106">[Sqoop] [ sqoop-user-guide-1.4.4] è un tootransfer strumento progettato dati tra i cluster Hadoop e database relazionali.</span><span class="sxs-lookup"><span data-stu-id="787aa-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="787aa-107">È possibile utilizzarlo tooimport dati da un sistema di gestione di database relazionali (RDBMS) ad esempio SQL Server, MySQL o Oracle in hello distributed file system Hadoop (HDFS), la trasformazione dei dati di hello in Hadoop MapReduce o Hive e quindi esportare i dati hello in un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="787aa-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="787aa-108">In questa esercitazione si userà un database SQL Server per il database relazionale.</span><span class="sxs-lookup"><span data-stu-id="787aa-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="787aa-109">Per le versioni Sqoop che sono supportate nei cluster HDInsight, vedere [novità introdotta nelle versioni di cluster hello fornite da HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="787aa-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="787aa-110">Comprendere scenario hello</span><span class="sxs-lookup"><span data-stu-id="787aa-110">Understand hello scenario</span></span>

<span data-ttu-id="787aa-111">Il cluster HDInsight include alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="787aa-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="787aa-112">Utilizzare hello due esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="787aa-112">You use hello following two samples:</span></span>

* <span data-ttu-id="787aa-113">Un file di log log4j presente in */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="787aa-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="787aa-114">Hello seguenti registri viene estratti dal file hello:</span><span class="sxs-lookup"><span data-stu-id="787aa-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="787aa-115">Una tabella Hive denominata *hivesampletable*, che i riferimenti hello file di dati si trova in */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="787aa-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="787aa-116">tabella Hello contiene alcuni dati del dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="787aa-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="787aa-117">Campo</span><span class="sxs-lookup"><span data-stu-id="787aa-117">Field</span></span> | <span data-ttu-id="787aa-118">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="787aa-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="787aa-119">clientid</span><span class="sxs-lookup"><span data-stu-id="787aa-119">clientid</span></span> |<span data-ttu-id="787aa-120">string</span><span class="sxs-lookup"><span data-stu-id="787aa-120">string</span></span> |
  | <span data-ttu-id="787aa-121">querytime</span><span class="sxs-lookup"><span data-stu-id="787aa-121">querytime</span></span> |<span data-ttu-id="787aa-122">string</span><span class="sxs-lookup"><span data-stu-id="787aa-122">string</span></span> |
  | <span data-ttu-id="787aa-123">market</span><span class="sxs-lookup"><span data-stu-id="787aa-123">market</span></span> |<span data-ttu-id="787aa-124">string</span><span class="sxs-lookup"><span data-stu-id="787aa-124">string</span></span> |
  | <span data-ttu-id="787aa-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="787aa-125">deviceplatform</span></span> |<span data-ttu-id="787aa-126">string</span><span class="sxs-lookup"><span data-stu-id="787aa-126">string</span></span> |
  | <span data-ttu-id="787aa-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="787aa-127">devicemake</span></span> |<span data-ttu-id="787aa-128">string</span><span class="sxs-lookup"><span data-stu-id="787aa-128">string</span></span> |
  | <span data-ttu-id="787aa-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="787aa-129">devicemodel</span></span> |<span data-ttu-id="787aa-130">string</span><span class="sxs-lookup"><span data-stu-id="787aa-130">string</span></span> |
  | <span data-ttu-id="787aa-131">state</span><span class="sxs-lookup"><span data-stu-id="787aa-131">state</span></span> |<span data-ttu-id="787aa-132">string</span><span class="sxs-lookup"><span data-stu-id="787aa-132">string</span></span> |
  | <span data-ttu-id="787aa-133">country</span><span class="sxs-lookup"><span data-stu-id="787aa-133">country</span></span> |<span data-ttu-id="787aa-134">string</span><span class="sxs-lookup"><span data-stu-id="787aa-134">string</span></span> |
  | <span data-ttu-id="787aa-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="787aa-135">querydwelltime</span></span> |<span data-ttu-id="787aa-136">double</span><span class="sxs-lookup"><span data-stu-id="787aa-136">double</span></span> |
  | <span data-ttu-id="787aa-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="787aa-137">sessionid</span></span> |<span data-ttu-id="787aa-138">bigint</span><span class="sxs-lookup"><span data-stu-id="787aa-138">bigint</span></span> |
  | <span data-ttu-id="787aa-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="787aa-139">sessionpagevieworder</span></span> |<span data-ttu-id="787aa-140">bigint</span><span class="sxs-lookup"><span data-stu-id="787aa-140">bigint</span></span> |

<span data-ttu-id="787aa-141">Esportare innanzitutto *sample.log* e *hivesampletable* toohello Azure SQL database o tooSQL Server e quindi Importa hello tabella che contiene i dati dei dispositivi mobili hello eseguire il backup tooHDInsight utilizzando hello percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="787aa-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="787aa-142">Creare un cluster e un database SQL</span><span class="sxs-lookup"><span data-stu-id="787aa-142">Create cluster and SQL database</span></span>
<span data-ttu-id="787aa-143">In questa sezione viene illustrato come toocreate un cluster, un Database SQL e schemi di database SQL di hello per l'utilizzo in esecuzione di esercitazione hello hello portale di Azure e un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="787aa-144">Hello è reperibile [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="787aa-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="787aa-145">il modello di gestione risorse di Hello chiama un database di tooSQL di bacpac pacchetto toodeploy hello tabella schemi.</span><span class="sxs-lookup"><span data-stu-id="787aa-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="787aa-146">pacchetto bacpac Hello si trova in un contenitore di blob pubblici, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="787aa-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="787aa-147">Se si desidera toouse un contenitore privato per i file bacpac hello, utilizzare hello valori hello modello seguente:</span><span class="sxs-lookup"><span data-stu-id="787aa-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="787aa-148">Se si preferisce toouse Azure PowerShell toocreate hello cluster e hello Database SQL, vedere [appendice](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="787aa-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="787aa-149">Fare clic su hello seguente immagine tooopen un modello di gestione risorse di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="787aa-150">Immettere hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="787aa-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="787aa-151">**Sottoscrizione**: immettere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="787aa-152">**Gruppo di risorse**: creare un nuovo gruppo di risorse di Azure o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="787aa-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="787aa-153">Un gruppo di risorse viene usato per finalità di gestione</span><span class="sxs-lookup"><span data-stu-id="787aa-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="787aa-154">come contenitore per gli oggetti.</span><span class="sxs-lookup"><span data-stu-id="787aa-154">It is a container for objects.</span></span>
    - <span data-ttu-id="787aa-155">**Località**: selezionare un'area.</span><span class="sxs-lookup"><span data-stu-id="787aa-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="787aa-156">**ClusterName**: immettere un nome per un cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="787aa-157">**Nome account di accesso e la password del cluster**: nome di account di accesso predefinito di hello è amministratore.</span><span class="sxs-lookup"><span data-stu-id="787aa-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="787aa-158">**Nome utente e password SSH**.</span><span class="sxs-lookup"><span data-stu-id="787aa-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="787aa-159">**SQL database server login name and password**(Nome utente e password di accesso al server di database SQL).</span><span class="sxs-lookup"><span data-stu-id="787aa-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="787aa-160">**percorso _artifacts**: utilizzare il valore di predefinito hello, a meno che non si desidera toouse file backpac in un percorso diverso.</span><span class="sxs-lookup"><span data-stu-id="787aa-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="787aa-161">**_artifacts Location Sas Token** (_Token di firma di accesso condiviso posizione elementi): lasciare vuoto.</span><span class="sxs-lookup"><span data-stu-id="787aa-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="787aa-162">**Nome del File Bacpac**: utilizzare il valore di predefinito hello, a meno che non si desidera toouse backpac un file personalizzato.</span><span class="sxs-lookup"><span data-stu-id="787aa-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="787aa-163">Hello i valori seguenti è hardcoded nella sezione variabili hello:</span><span class="sxs-lookup"><span data-stu-id="787aa-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="787aa-164">Nome dell'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="787aa-164">Default storage account name</span></span> | <span data-ttu-id="787aa-165"><CluterName>archivio</span><span class="sxs-lookup"><span data-stu-id="787aa-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="787aa-166">Nome server del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="787aa-166">Azure SQL database server name</span></span> |<span data-ttu-id="787aa-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="787aa-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="787aa-168">Nome del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="787aa-168">Azure SQL database name</span></span> |<span data-ttu-id="787aa-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="787aa-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="787aa-170">Annotare questi valori.</span><span class="sxs-lookup"><span data-stu-id="787aa-170">Please write down these values.</span></span>  <span data-ttu-id="787aa-171">È necessario più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="787aa-172">3. fare clic su **OK** parametri hello toosave.</span><span class="sxs-lookup"><span data-stu-id="787aa-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="787aa-173">4 da hello **distribuzione personalizzata** pannello, fare clic su **gruppo di risorse** elenco a discesa e quindi scegliere **New** toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="787aa-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="787aa-174">gruppo di risorse Hello è un contenitore che raggruppa i cluster di hello, account di archiviazione dipendenti hello e altre risorse collegate.</span><span class="sxs-lookup"><span data-stu-id="787aa-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="787aa-175">5. Fare clic su **Note legali** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="787aa-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="787aa-176">6. Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="787aa-176">6.Click **Create**.</span></span> <span data-ttu-id="787aa-177">Viene visualizzato un nuovo riquadro denominato Invio della distribuzione per Distribuzione modello.</span><span class="sxs-lookup"><span data-stu-id="787aa-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="787aa-178">Richiede circa cluster hello toocreate di circa 20 minuti e il database SQL.</span><span class="sxs-lookup"><span data-stu-id="787aa-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="787aa-179">Se si sceglie di database SQL di Azure esistente toouse o Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="787aa-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="787aa-180">**Database SQL di Azure**: È necessario configurare una regola del firewall per l'accesso di SQL Azure database server tooallow hello dalla propria workstation.</span><span class="sxs-lookup"><span data-stu-id="787aa-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="787aa-181">Per istruzioni sulla creazione di un database SQL di Azure e configurazione di firewall hello, vedere [iniziare a usare database SQL di Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="787aa-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="787aa-182">Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="787aa-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="787aa-183">Se questa impostazione del firewall è disabilitata, è necessario tooenable dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="787aa-184">Per istruzioni sulla creazione di un database SQL di Azure e sulla configurazione di regole del firewall, vedere l'articolo su come [creare e configurare un database SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="787aa-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="787aa-185">**SQL Server**: se il cluster HDInsight su hello stessa rete virtuale in Azure come SQL Server, è possibile utilizzare i passaggi di hello in questo articolo tooimport ed esportazione dati tooa database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787aa-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="787aa-186">HDInsight supporta solo reti virtuali basate sulla posizione e attualmente non funziona con le reti virtuali basate su gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="787aa-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="787aa-187">toocreate e configurare una rete virtuale, vedere [creare una rete virtuale usando il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="787aa-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="787aa-188">Quando si utilizza SQL Server nel Data Center, è necessario configurare la rete virtuale di hello come *site-to-site* o *point-to-site*.</span><span class="sxs-lookup"><span data-stu-id="787aa-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="787aa-189">Per **point-to-site** reti virtuali, SQL Server devono essere in esecuzione il client VPN di hello applicazione di configurazione, è disponibile da hello **Dashboard** della configurazione di rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="787aa-190">Quando si utilizza SQL Server in una macchina virtuale di Azure, è possibile utilizzare qualsiasi configurazione di rete virtuale se macchina virtuale hello che ospita SQL Server è un membro di hello stessa rete virtuale di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="787aa-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="787aa-191">toocreate un cluster HDInsight in una rete virtuale, vedere [cluster creare Hadoop in HDInsight mediante le opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="787aa-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="787aa-192">SQL Server deve sempre consentire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="787aa-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="787aa-193">È necessario utilizzare un Server SQL hello toocomplete account di accesso i passaggi in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="787aa-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="787aa-194">Eseguire processi Sqoop</span><span class="sxs-lookup"><span data-stu-id="787aa-194">Run Sqoop jobs</span></span>
<span data-ttu-id="787aa-195">HDInsight è in grado di eseguire processi Sqoop in vari modi.</span><span class="sxs-lookup"><span data-stu-id="787aa-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="787aa-196">Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="787aa-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="787aa-197">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="787aa-197">**Use this** if you want...</span></span> | <span data-ttu-id="787aa-198">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="787aa-198">...an **interactive** shell</span></span> | <span data-ttu-id="787aa-199">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="787aa-199">...**batch** processing</span></span> | <span data-ttu-id="787aa-200">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="787aa-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="787aa-201">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="787aa-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="787aa-202">SSH</span><span class="sxs-lookup"><span data-stu-id="787aa-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="787aa-203">✔</span><span class="sxs-lookup"><span data-stu-id="787aa-203">✔</span></span> |<span data-ttu-id="787aa-204">✔</span><span class="sxs-lookup"><span data-stu-id="787aa-204">✔</span></span> |<span data-ttu-id="787aa-205">Linux</span><span class="sxs-lookup"><span data-stu-id="787aa-205">Linux</span></span> |<span data-ttu-id="787aa-206">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="787aa-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="787aa-207">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="787aa-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="787aa-208">✔</span><span class="sxs-lookup"><span data-stu-id="787aa-208">✔</span></span> |<span data-ttu-id="787aa-209">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="787aa-209">Linux or Windows</span></span> |<span data-ttu-id="787aa-210">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="787aa-210">Windows (for now)</span></span> |
| [<span data-ttu-id="787aa-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="787aa-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="787aa-212">✔</span><span class="sxs-lookup"><span data-stu-id="787aa-212">✔</span></span> |<span data-ttu-id="787aa-213">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="787aa-213">Linux or Windows</span></span> |<span data-ttu-id="787aa-214">Windows</span><span class="sxs-lookup"><span data-stu-id="787aa-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="787aa-215">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="787aa-215">Limitations</span></span>
* <span data-ttu-id="787aa-216">Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.</span><span class="sxs-lookup"><span data-stu-id="787aa-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="787aa-217">Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop esegue più inserimenti anziché l'invio in batch le operazioni di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="787aa-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="787aa-218">Next steps</span></span>
<span data-ttu-id="787aa-219">Ora si è appreso come toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="787aa-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="787aa-220">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="787aa-220">toolearn more, see:</span></span>

* [<span data-ttu-id="787aa-221">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="787aa-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="787aa-222">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="787aa-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="787aa-223">[Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="787aa-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="787aa-224">[Analizzare i dati di ritardo volo tramite HDInsight][hdinsight-analyze-flight-data]: utilizzare Hive volo tooanalyze ritardare dati e quindi utilizzare il database SQL di Azure tooan di Sqoop tooexport dati.</span><span class="sxs-lookup"><span data-stu-id="787aa-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="787aa-225">[Caricare dati tooHDInsight][hdinsight-upload-data]: trovare altri metodi per il caricamento di archiviazione Blob di dati tooHDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="787aa-226">Appendice A - Esempio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="787aa-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="787aa-227">esempio di PowerShell Hello esegue hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="787aa-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="787aa-228">Connettersi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="787aa-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="787aa-229">Creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-229">Create an Azure resource group.</span></span> <span data-ttu-id="787aa-230">Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="787aa-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="787aa-231">Creare un server di Database SQL di Azure, un database SQL Azure e due tabelle.</span><span class="sxs-lookup"><span data-stu-id="787aa-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="787aa-232">Se invece si usa SQL Server, utilizzare hello le tabelle di hello toocreate le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="787aa-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="787aa-233">tabelle e database hello più semplice modo tooexamine hello è toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="787aa-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="787aa-234">server di database di Hello e hello database possono essere esaminati tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="787aa-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="787aa-235">Creare un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="787aa-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="787aa-236">cluster hello tooexamine, è possibile utilizzare hello portale di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="787aa-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="787aa-237">File di dati di origine hello pre-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="787aa-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="787aa-238">In questa esercitazione, si esporta un file di log log4j (un file delimitato da virgole) e un database di SQL Azure tooan tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="787aa-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="787aa-239">Hello file delimitato viene chiamato */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="787aa-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="787aa-240">In precedenza nell'esercitazione di hello, si è visto alcuni esempi dei registri log4j.</span><span class="sxs-lookup"><span data-stu-id="787aa-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="787aa-241">Nel file di log hello, esistono alcune righe vuote e alcuni toothese simile righe:</span><span class="sxs-lookup"><span data-stu-id="787aa-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="787aa-242">L'operazione è corretta per altri esempi che utilizzano questo tipo di dati, ma è necessario rimuovere queste eccezioni prima sarà possibile importare in database SQL di Azure hello o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787aa-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="787aa-243">Sqoop esportazione ha esito negativo se è presente una stringa vuota o una riga con meno elementi numero hello di campi definiti nella tabella di database SQL di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="787aa-244">tabella log4jlogs Hello è 7 campi di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="787aa-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="787aa-245">Questa procedura crea un nuovo file nel cluster hello: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="787aa-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="787aa-246">file di dati modificati hello tooexamine, è possibile utilizzare hello portale di Azure, uno strumento di esplorazione di archiviazione di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="787aa-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="787aa-247">[Guida introduttiva di HDInsight] [ hdinsight-get-started] dispone di un codice di esempio per l'utilizzo di Azure PowerShell toodownload un file e visualizzare il contenuto di file hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="787aa-248">Esportare un database di SQL Azure toohello file di dati.</span><span class="sxs-lookup"><span data-stu-id="787aa-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="787aa-249">file di origine Hello è tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="787aa-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="787aa-250">Hello tabella in cui hello dati esportati toois chiamato log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="787aa-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="787aa-251">Diverso da informazioni sulla stringa di connessione, i passaggi hello in questa sezione dovrebbero funzionare per un database SQL di Azure o per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="787aa-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="787aa-252">Questi passaggi sono stati testati tramite hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="787aa-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="787aa-253">**Configurazione di rete virtuale di Azure point-to-site**: una rete virtuale connessa hello HDInsight cluster tooa SQL Server in un centro dati privato.</span><span class="sxs-lookup"><span data-stu-id="787aa-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="787aa-254">Vedere [configurare una VPN Point-to-Site nel portale di gestione di hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="787aa-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="787aa-255">**Azure HDInsight 3.1**: per informazioni sulla creazione di un cluster in una rete virtuale, vedere l'articolo relativo alla [creazione di cluster Hadoop in HDInsight con opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md) .</span><span class="sxs-lookup"><span data-stu-id="787aa-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="787aa-256">**SQL Server 2014**: configurato in modo sicuro l'autenticazione tooallow e in esecuzione hello VPN client configurazione pacchetto tooconnect toohello di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="787aa-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="787aa-257">Esportare un database di SQL Azure toohello tabella Hive.</span><span class="sxs-lookup"><span data-stu-id="787aa-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="787aa-258">Importare il cluster HDInsight toohello di hello mobiledata tabella.</span><span class="sxs-lookup"><span data-stu-id="787aa-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="787aa-259">file di dati modificati hello tooexamine, è possibile utilizzare hello portale di Azure, uno strumento di esplorazione di archiviazione di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="787aa-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="787aa-260">[Guida introduttiva di HDInsight] [ hdinsight-get-started] dispone di un codice di esempio sull'uso di Azure PowerShell toodownload un file e visualizzare il contenuto di file hello.</span><span class="sxs-lookup"><span data-stu-id="787aa-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="787aa-261">esempio di PowerShell Hello</span><span class="sxs-lookup"><span data-stu-id="787aa-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
