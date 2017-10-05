---
title: Eseguire processi Apache Sqoop con Azure HDInsight (Hadoop) | Microsoft Docs
description: Informazioni su come usare Azure PowerShell da una workstation per eseguire importazioni ed esportazioni con Sqoop tra un cluster Hadoop e un database SQL di Azure.
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
ms.openlocfilehash: 8e77153493b6f37f5f48116b86bad6b25a50d1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="1acc5-103">Usare Sqoop con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="1acc5-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="1acc5-104">Informazioni su come usare Sqoop in HDInsight per effettuare importazioni ed esportazioni tra un cluster HDInsight e un database SQL di Azure o un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acc5-104">Learn how to use Sqoop in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="1acc5-105">Benché Hadoop rappresenti una scelta ottimale per l'elaborazione di dati non strutturati e semistrutturati, ad esempio log e file, potrebbe essere necessario elaborare anche dati strutturati archiviati in database relazionali.</span><span class="sxs-lookup"><span data-stu-id="1acc5-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="1acc5-106">[Sqoop][sqoop-user-guide-1.4.4] è uno strumento progettato per il trasferimento di dati tra cluster Hadoop e database relazionali.</span><span class="sxs-lookup"><span data-stu-id="1acc5-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed to transfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="1acc5-107">Può essere usato per importare dati in HDFS (Hadoop Distributed File System) da un sistema di gestione di database relazionali (RDBMS), ad esempio SQL, MySQL oppure Oracle, trasformare i dati in Hadoop con MapReduce o Hive e quindi esportarli nuovamente in un sistema RDBMS.</span><span class="sxs-lookup"><span data-stu-id="1acc5-107">You can use it to import data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span> <span data-ttu-id="1acc5-108">In questa esercitazione si userà un database SQL Server per il database relazionale.</span><span class="sxs-lookup"><span data-stu-id="1acc5-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="1acc5-109">Per informazioni sulle versioni di Sqoop supportate nei cluster HDInsight, vedere l'articolo relativo alle [novità delle versioni cluster incluse in HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="1acc5-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-the-scenario"></a><span data-ttu-id="1acc5-110">Informazioni sullo scenario</span><span class="sxs-lookup"><span data-stu-id="1acc5-110">Understand the scenario</span></span>

<span data-ttu-id="1acc5-111">Il cluster HDInsight include alcuni dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="1acc5-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="1acc5-112">Usare i due esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1acc5-112">You use the following two samples:</span></span>

* <span data-ttu-id="1acc5-113">Un file di log log4j presente in */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="1acc5-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="1acc5-114">Dal file verranno estratti i log seguenti:</span><span class="sxs-lookup"><span data-stu-id="1acc5-114">The following logs are extracted from the file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="1acc5-115">Una tabella di Hive denominata *hivesampletable*, che fa riferimento al file di dati presente in */hive/warehouse/hivesampletable*.</span><span class="sxs-lookup"><span data-stu-id="1acc5-115">A Hive table named *hivesampletable*, which references the data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="1acc5-116">La tabella contiene alcuni dati relativi al dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="1acc5-116">The table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="1acc5-117">Campo</span><span class="sxs-lookup"><span data-stu-id="1acc5-117">Field</span></span> | <span data-ttu-id="1acc5-118">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="1acc5-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="1acc5-119">clientid</span><span class="sxs-lookup"><span data-stu-id="1acc5-119">clientid</span></span> |<span data-ttu-id="1acc5-120">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-120">string</span></span> |
  | <span data-ttu-id="1acc5-121">querytime</span><span class="sxs-lookup"><span data-stu-id="1acc5-121">querytime</span></span> |<span data-ttu-id="1acc5-122">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-122">string</span></span> |
  | <span data-ttu-id="1acc5-123">market</span><span class="sxs-lookup"><span data-stu-id="1acc5-123">market</span></span> |<span data-ttu-id="1acc5-124">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-124">string</span></span> |
  | <span data-ttu-id="1acc5-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="1acc5-125">deviceplatform</span></span> |<span data-ttu-id="1acc5-126">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-126">string</span></span> |
  | <span data-ttu-id="1acc5-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="1acc5-127">devicemake</span></span> |<span data-ttu-id="1acc5-128">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-128">string</span></span> |
  | <span data-ttu-id="1acc5-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="1acc5-129">devicemodel</span></span> |<span data-ttu-id="1acc5-130">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-130">string</span></span> |
  | <span data-ttu-id="1acc5-131">state</span><span class="sxs-lookup"><span data-stu-id="1acc5-131">state</span></span> |<span data-ttu-id="1acc5-132">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-132">string</span></span> |
  | <span data-ttu-id="1acc5-133">country</span><span class="sxs-lookup"><span data-stu-id="1acc5-133">country</span></span> |<span data-ttu-id="1acc5-134">string</span><span class="sxs-lookup"><span data-stu-id="1acc5-134">string</span></span> |
  | <span data-ttu-id="1acc5-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="1acc5-135">querydwelltime</span></span> |<span data-ttu-id="1acc5-136">double</span><span class="sxs-lookup"><span data-stu-id="1acc5-136">double</span></span> |
  | <span data-ttu-id="1acc5-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="1acc5-137">sessionid</span></span> |<span data-ttu-id="1acc5-138">bigint</span><span class="sxs-lookup"><span data-stu-id="1acc5-138">bigint</span></span> |
  | <span data-ttu-id="1acc5-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="1acc5-139">sessionpagevieworder</span></span> |<span data-ttu-id="1acc5-140">bigint</span><span class="sxs-lookup"><span data-stu-id="1acc5-140">bigint</span></span> |

<span data-ttu-id="1acc5-141">Prima di tutto, esportare *sample.log* e *hivesampletable* nel database SQL di Azure o in SQL Server e quindi importare di nuovo in HDInsight la tabella contenente i dati del dispositivo mobile usando il percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="1acc5-141">First, you export *sample.log* and *hivesampletable* to the Azure SQL database or to SQL Server, and then import the table that contains the mobile device data back to HDInsight by using the following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="1acc5-142">Creare un cluster e un database SQL</span><span class="sxs-lookup"><span data-stu-id="1acc5-142">Create cluster and SQL database</span></span>
<span data-ttu-id="1acc5-143">Questa sezione illustra come creare un cluster, un database SQL e gli schemi del database SQL per eseguire l'esercitazione con il portale di Azure e un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1acc5-143">This section shows you how to create a cluster, a SQL Database, and the SQL database schemas for running the tutorial using the Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="1acc5-144">Il modello è disponibile tra i [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="1acc5-144">The template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="1acc5-145">Il modello di Resource Manager chiama un pacchetto bacpac per distribuire gli schemi della tabella nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="1acc5-145">The Resource Manager template calls a bacpac package to deploy the table schemas to SQL database.</span></span>  <span data-ttu-id="1acc5-146">Il pacchetto bacpac si trova in un contenitore BLOB pubblico, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span><span class="sxs-lookup"><span data-stu-id="1acc5-146">The bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="1acc5-147">Se si vuole usare un contenitore privato per i file bacpac, usare i valori seguenti nel modello:</span><span class="sxs-lookup"><span data-stu-id="1acc5-147">If you want to use a private container for the bacpac files, use the following values in the template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="1acc5-148">Se si preferisce usare Azure PowerShell per creare il cluster e il database SQL, vedere l'[appendice A](#appendix-a---a-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="1acc5-148">If you prefer to use Azure PowerShell to create the cluster and the SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="1acc5-149">Fare clic sull'immagine seguente per aprire un modello di Resource Manager nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-149">Click the following image to open a Resource Manager template in the Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy to Azure"></a>
   

2. <span data-ttu-id="1acc5-150">Immettere le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="1acc5-150">Enter the following properties:</span></span>

    - <span data-ttu-id="1acc5-151">**Sottoscrizione**: immettere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="1acc5-152">**Gruppo di risorse**: creare un nuovo gruppo di risorse di Azure o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="1acc5-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="1acc5-153">Un gruppo di risorse viene usato per finalità di gestione</span><span class="sxs-lookup"><span data-stu-id="1acc5-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="1acc5-154">come contenitore per gli oggetti.</span><span class="sxs-lookup"><span data-stu-id="1acc5-154">It is a container for objects.</span></span>
    - <span data-ttu-id="1acc5-155">**Località**: selezionare un'area.</span><span class="sxs-lookup"><span data-stu-id="1acc5-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="1acc5-156">**Nome del cluster**: immettere un nome per il cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1acc5-156">**ClusterName**: Enter a name for the Hadoop cluster.</span></span>
    - <span data-ttu-id="1acc5-157">**Nome utente e password di accesso del cluster**: il nome dell'account di accesso predefinito è admin.</span><span class="sxs-lookup"><span data-stu-id="1acc5-157">**Cluster login name and password**: The default login name is admin.</span></span>
    - <span data-ttu-id="1acc5-158">**SSH user name and password**(Nome utente e password SSH).</span><span class="sxs-lookup"><span data-stu-id="1acc5-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="1acc5-159">**SQL database server login name and password**(Nome utente e password di accesso al server di database SQL).</span><span class="sxs-lookup"><span data-stu-id="1acc5-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="1acc5-160">**_artifacts Location** (_Posizione elementi): usare il valore predefinito, a meno che non si voglia usare un file BACPAC in una diversa posizione.</span><span class="sxs-lookup"><span data-stu-id="1acc5-160">**_artifacts Location**: Use the default value unless you want to use your own backpac file in a different location.</span></span>
    - <span data-ttu-id="1acc5-161">**_artifacts Location Sas Token** (_Token di firma di accesso condiviso posizione elementi): lasciare vuoto.</span><span class="sxs-lookup"><span data-stu-id="1acc5-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="1acc5-162">**Bacpac File Name** (Nome file BACPAC): usare il valore predefinito, a meno che non si voglia usare un proprio file BACPAC.</span><span class="sxs-lookup"><span data-stu-id="1acc5-162">**Bacpac File Name**: Use the default value unless you want to use your own backpac file.</span></span>
     
     <span data-ttu-id="1acc5-163">I valori seguenti sono hardcoded nella sezione relativa alle variabili:</span><span class="sxs-lookup"><span data-stu-id="1acc5-163">The following values are hardcoded in the variables section:</span></span>
     
     | <span data-ttu-id="1acc5-164">Nome dell'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="1acc5-164">Default storage account name</span></span> | <span data-ttu-id="1acc5-165"><CluterName>archivio</span><span class="sxs-lookup"><span data-stu-id="1acc5-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="1acc5-166">Nome server del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="1acc5-166">Azure SQL database server name</span></span> |<span data-ttu-id="1acc5-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="1acc5-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="1acc5-168">Nome del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="1acc5-168">Azure SQL database name</span></span> |<span data-ttu-id="1acc5-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="1acc5-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="1acc5-170">Annotare questi valori.</span><span class="sxs-lookup"><span data-stu-id="1acc5-170">Please write down these values.</span></span>  <span data-ttu-id="1acc5-171">perché sarà necessario usarli più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1acc5-171">You need them later in the tutorial.</span></span>

<span data-ttu-id="1acc5-172">3. Fare clic su **OK** per salvare i parametri.</span><span class="sxs-lookup"><span data-stu-id="1acc5-172">3.Click **OK** to save the parameters.</span></span>

<span data-ttu-id="1acc5-173">4. Nel pannello **Distribuzione personalizzata** fare clic su **Gruppo di risorse** nella casella di riepilogo a discesa e quindi scegliere **Nuovo** per creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1acc5-173">4.From the **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** to create a new resource group.</span></span> <span data-ttu-id="1acc5-174">Il gruppo di risorse è un contenitore che raggruppa il cluster, l'account di archiviazione dipendente e altre risorse collegate.</span><span class="sxs-lookup"><span data-stu-id="1acc5-174">The resource group is a container that groups the cluster, the dependent storage account and other linked resource.</span></span>

<span data-ttu-id="1acc5-175">5. Fare clic su **Note legali** e quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1acc5-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="1acc5-176">6. Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1acc5-176">6.Click **Create**.</span></span> <span data-ttu-id="1acc5-177">Viene visualizzato un nuovo riquadro denominato Invio della distribuzione per Distribuzione modello.</span><span class="sxs-lookup"><span data-stu-id="1acc5-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="1acc5-178">La creazione del cluster e del database SQL richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="1acc5-178">It takes about around 20 minutes to create the cluster and SQL database.</span></span>

<span data-ttu-id="1acc5-179">Se si sceglie di utilizzare un database SQL di Azure esistente o un Server SQL di Microsoft</span><span class="sxs-lookup"><span data-stu-id="1acc5-179">If you choose to use existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="1acc5-180">**Database SQL di Azure**: è necessario configurare una regola del firewall per il server di database SQL per consentire l'accesso dalla workstation.</span><span class="sxs-lookup"><span data-stu-id="1acc5-180">**Azure SQL database**: You must configure a firewall rule for the Azure SQL database server to allow access from your workstation.</span></span> <span data-ttu-id="1acc5-181">Per istruzioni sulla creazione di un database SQL di Azure e sulla configurazione del firewall, vedere l'[introduzione all'uso del database SQL di Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="1acc5-181">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="1acc5-182">Per impostazione predefinita, un database SQL di Azure consente connessioni da servizi di Azure, ad esempio Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="1acc5-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="1acc5-183">Se questa impostazione del firewall è disabilitata, è necessario abilitarla dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-183">If this firewall setting is disabled, you need to enable it from the Azure portal.</span></span> <span data-ttu-id="1acc5-184">Per istruzioni sulla creazione di un database SQL di Azure e sulla configurazione di regole del firewall, vedere l'articolo su come [creare e configurare un database SQL][sqldatabase-create-configue].</span><span class="sxs-lookup"><span data-stu-id="1acc5-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="1acc5-185">**SQL Server**: se il cluster HDInsight si trova sulla stessa rete virtuale di Azure di SQL Server, è possibile usare la procedura descritta in questo articolo per importare ed esportare i dati in un database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acc5-185">**SQL Server**: If your HDInsight cluster is on the same virtual network in Azure as SQL Server, you can use the steps in this article to import and export data to a SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="1acc5-186">HDInsight supporta solo reti virtuali basate sulla posizione e attualmente non funziona con le reti virtuali basate su gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="1acc5-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="1acc5-187">Per creare e configurare una rete virtuale, vedere [Creare una rete virtuale usando il portale di Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1acc5-187">To create and configure a virtual network, see [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="1acc5-188">Quando si usa SQL Server nel proprio data center, è necessario configurare la rete virtuale come *da sito a sito* o *da punto a sito*.</span><span class="sxs-lookup"><span data-stu-id="1acc5-188">When you are using SQL Server in your datacenter, you must configure the virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="1acc5-189">Per le reti virtuali **da punto a sito**, è necessario che su SQL Server venga eseguita l'applicazione di configurazione del client VPN, disponibile nel **Dashboard** di configurazione della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-189">For **point-to-site** virtual networks, SQL Server must be running the VPN client configuration application, which is available from the **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="1acc5-190">Quando si usa SQL Server in una macchina virtuale di Azure, sarà possibile usare qualsiasi configurazione di rete virtuale a condizione che la macchina virtuale sulla quale è ospitato SQL Server sia un membro della stessa rete virtuale di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1acc5-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if the virtual machine hosting SQL Server is a member of the same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="1acc5-191">Per creare un cluster HDInsight in una rete virtuale, vedere l'articolo relativo alla [creazione di cluster Hadoop in HDInsight con opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="1acc5-191">To create an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1acc5-192">SQL Server deve sempre consentire l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1acc5-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="1acc5-193">Per la procedura descritta in questo articolo è necessario usare un account di accesso di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acc5-193">You must use a SQL Server login to complete the steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="1acc5-194">Eseguire processi Sqoop</span><span class="sxs-lookup"><span data-stu-id="1acc5-194">Run Sqoop jobs</span></span>
<span data-ttu-id="1acc5-195">HDInsight è in grado di eseguire processi Sqoop in vari modi.</span><span class="sxs-lookup"><span data-stu-id="1acc5-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="1acc5-196">Usare la tabella seguente per decidere il metodo più adatto alle proprie esigenze, quindi fare clic sul collegamento per visualizzare una procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="1acc5-196">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="1acc5-197">**Usare questo** se si desidera...</span><span class="sxs-lookup"><span data-stu-id="1acc5-197">**Use this** if you want...</span></span> | <span data-ttu-id="1acc5-198">...una shell **interattiva**</span><span class="sxs-lookup"><span data-stu-id="1acc5-198">...an **interactive** shell</span></span> | <span data-ttu-id="1acc5-199">...elaborazione**batch**</span><span class="sxs-lookup"><span data-stu-id="1acc5-199">...**batch** processing</span></span> | <span data-ttu-id="1acc5-200">...con questo **sistema operativo cluster**</span><span class="sxs-lookup"><span data-stu-id="1acc5-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="1acc5-201">...da questo **sistema operativo client**</span><span class="sxs-lookup"><span data-stu-id="1acc5-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="1acc5-202">SSH</span><span class="sxs-lookup"><span data-stu-id="1acc5-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="1acc5-203">✔</span><span class="sxs-lookup"><span data-stu-id="1acc5-203">✔</span></span> |<span data-ttu-id="1acc5-204">✔</span><span class="sxs-lookup"><span data-stu-id="1acc5-204">✔</span></span> |<span data-ttu-id="1acc5-205">Linux</span><span class="sxs-lookup"><span data-stu-id="1acc5-205">Linux</span></span> |<span data-ttu-id="1acc5-206">Linux, Unix, Mac OS X o Windows</span><span class="sxs-lookup"><span data-stu-id="1acc5-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1acc5-207">.NET SDK per Hadoop</span><span class="sxs-lookup"><span data-stu-id="1acc5-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="1acc5-208">✔</span><span class="sxs-lookup"><span data-stu-id="1acc5-208">✔</span></span> |<span data-ttu-id="1acc5-209">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="1acc5-209">Linux or Windows</span></span> |<span data-ttu-id="1acc5-210">Windows (per ora)</span><span class="sxs-lookup"><span data-stu-id="1acc5-210">Windows (for now)</span></span> |
| [<span data-ttu-id="1acc5-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1acc5-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="1acc5-212">✔</span><span class="sxs-lookup"><span data-stu-id="1acc5-212">✔</span></span> |<span data-ttu-id="1acc5-213">Linux o Windows</span><span class="sxs-lookup"><span data-stu-id="1acc5-213">Linux or Windows</span></span> |<span data-ttu-id="1acc5-214">Windows</span><span class="sxs-lookup"><span data-stu-id="1acc5-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="1acc5-215">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="1acc5-215">Limitations</span></span>
* <span data-ttu-id="1acc5-216">Esportazione di massa: con HDInsight basato su Linux, attualmente il connettore Sqoop, usato per esportare dati in Microsoft SQL Server o nel database SQL di Azure, non supporta inserimenti di massa.</span><span class="sxs-lookup"><span data-stu-id="1acc5-216">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="1acc5-217">Invio in batch: con HDInsight basato su Linux, quando si usa il comando `-batch` durante gli inserimenti, Sqoop esegue più inserimenti invece di suddividere in batch le operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="1acc5-217">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1acc5-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1acc5-218">Next steps</span></span>
<span data-ttu-id="1acc5-219">In questa esercitazione si è appreso come usare Sqoop.</span><span class="sxs-lookup"><span data-stu-id="1acc5-219">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="1acc5-220">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="1acc5-220">To learn more, see:</span></span>

* [<span data-ttu-id="1acc5-221">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1acc5-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1acc5-222">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="1acc5-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="1acc5-223">[Usare Oozie con HDInsight][hdinsight-use-oozie]: usare un'azione di Sqoop nel flusso di lavoro di Oozie.</span><span class="sxs-lookup"><span data-stu-id="1acc5-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="1acc5-224">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-data]: usare Hive per analizzare i dati sui ritardi dei voli e quindi usare Sqoop per esportare dati in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="1acc5-225">[Caricare dati in HDInsight][hdinsight-upload-data]: altri metodi per caricare dati in HDInsight e nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-225">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="1acc5-226">Appendice A - Esempio di PowerShell</span><span class="sxs-lookup"><span data-stu-id="1acc5-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="1acc5-227">L'esempio di PowerShell esegue questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1acc5-227">The PowerShell sample performs the following steps:</span></span>

1. <span data-ttu-id="1acc5-228">Connettersi ad Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-228">Connect to Azure.</span></span>
2. <span data-ttu-id="1acc5-229">Creare un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-229">Create an Azure resource group.</span></span> <span data-ttu-id="1acc5-230">Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1acc5-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="1acc5-231">Creare un server di Database SQL di Azure, un database SQL Azure e due tabelle.</span><span class="sxs-lookup"><span data-stu-id="1acc5-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="1acc5-232">Se invece si utilizza SQL Server, utilizzare le istruzioni seguenti per creare le tabelle:</span><span class="sxs-lookup"><span data-stu-id="1acc5-232">If you use SQL Server instead, use the following statements to create the tables:</span></span>
   
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
   
    <span data-ttu-id="1acc5-233">Il modo più semplice per esaminare il database e le tabelle è quello di usare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1acc5-233">The easiest way to examine the database and tables is to use Visual Studio.</span></span> <span data-ttu-id="1acc5-234">Il server del database e il database possono essere esaminati tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-234">The database server and the database can be examined using the Azure portal.</span></span>
4. <span data-ttu-id="1acc5-235">Creare un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="1acc5-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="1acc5-236">Per esaminare il cluster, è possibile usare il portale di Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1acc5-236">To examine the cluster, you can use the Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="1acc5-237">Pre-elaborare i file dei dati di origine.</span><span class="sxs-lookup"><span data-stu-id="1acc5-237">Pre-process the source data file.</span></span>
   
    <span data-ttu-id="1acc5-238">In questa esercitazione nel database SQL di Azure vengono esportati un file di log log4j (un file con valori delimitati) e una tabella di Hive.</span><span class="sxs-lookup"><span data-stu-id="1acc5-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table to an Azure SQL database.</span></span> <span data-ttu-id="1acc5-239">Il file con valori delimitati è denominato */example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="1acc5-239">The delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="1acc5-240">Alcuni esempi di file di log log4j sono stati visualizzati in precedenza in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1acc5-240">Earlier in the tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="1acc5-241">Nel file di log sono presenti alcune righe vuote e righe simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="1acc5-241">In the log file, there are some empty lines and some lines similar to these:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="1acc5-242">Questa condizione può andar bene per altri esempi in cui vengono usati questi dati, ma è necessario rimuovere queste eccezioni prima di poterli importare nel database SQL di Azure o in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acc5-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into the Azure SQL database or SQL Server.</span></span> <span data-ttu-id="1acc5-243">In presenza di una stringa vuota o di una riga contenente un numero di elementi inferiore al numero dei campi definiti nella tabella del database SQL di Azure, non è possibile eseguire l'esportazione con Sqoop.</span><span class="sxs-lookup"><span data-stu-id="1acc5-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than the number of fields defined in the Azure SQL database table.</span></span> <span data-ttu-id="1acc5-244">La tabella log4jlogs comprende 7 campi tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="1acc5-244">The log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="1acc5-245">Questa procedura crea un nuovo file nel cluster: tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="1acc5-245">This procedure creates a new file on the cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="1acc5-246">Per esaminare il file di dati modificato, è possibile usare il portale di Azure, uno strumento di Esplora archivi Azure oppure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1acc5-246">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="1acc5-247">Nell'[introduzione a HDInsight][hdinsight-get-started] è riportato un esempio di codice per usare Azure PowerShell per scaricare un file e visualizzarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1acc5-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell to download a file and display the file content.</span></span>
6. <span data-ttu-id="1acc5-248">Esportare un file dei dati nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-248">Export a data file to the Azure SQL database.</span></span>
   
    <span data-ttu-id="1acc5-249">Il file di origine è tutorials/usesqoop/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="1acc5-249">The source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="1acc5-250">La tabella in cui vengono esportati i dati è denominata log4jlogs.</span><span class="sxs-lookup"><span data-stu-id="1acc5-250">The table where the data is exported to is called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1acc5-251">Ad eccezione delle informazioni sulla stringa di connessione, la procedura descritta in questa sezione dovrebbe funzionare per il database SQL di Azure e per SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1acc5-251">Other than connection string information, the steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="1acc5-252">La procedura è stata verificata con la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="1acc5-252">These steps were tested by using the following configuration:</span></span>
   > 
   > * <span data-ttu-id="1acc5-253">**Configurazione da punto a sito della rete virtuale di Azure**: una rete virtuale che connette il cluster HDInsight a un SQL Server in un data center privato.</span><span class="sxs-lookup"><span data-stu-id="1acc5-253">**Azure virtual network point-to-site configuration**: A virtual network connected the HDInsight cluster to a SQL Server in a private datacenter.</span></span> <span data-ttu-id="1acc5-254">Per altre informazioni, vedere [Configurare una VPN da punto a sito nel portale di gestione](../vpn-gateway/vpn-gateway-point-to-site-create.md) .</span><span class="sxs-lookup"><span data-stu-id="1acc5-254">See [Configure a Point-to-Site VPN in the Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="1acc5-255">**Azure HDInsight 3.1**: per informazioni sulla creazione di un cluster in una rete virtuale, vedere l'articolo relativo alla [creazione di cluster Hadoop in HDInsight con opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md) .</span><span class="sxs-lookup"><span data-stu-id="1acc5-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="1acc5-256">**SQL Server 2014**: configurato per consentire l'autenticazione SQL e l'esecuzione del pacchetto di configurazione del client VPN per eseguire la connessione sicura alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1acc5-256">**SQL Server 2014**: Configured to allow authentication and running the VPN client configuration package to connect securely to the virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="1acc5-257">Esportare una tabella Hive nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acc5-257">Export a Hive table to the Azure SQL database.</span></span>
8. <span data-ttu-id="1acc5-258">Importare la tabella mobiledata nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1acc5-258">Import the mobiledata table to the HDInsight cluster.</span></span>
   
    <span data-ttu-id="1acc5-259">Per esaminare il file di dati modificato, è possibile usare il portale di Azure, uno strumento di Esplora archivi Azure oppure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1acc5-259">To examine the modified data file, you can use the Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="1acc5-260">Nell'[introduzione a HDInsight][hdinsight-get-started] è riportato un esempio di codice relativo all'uso di Azure PowerShell per scaricare un file e visualizzarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1acc5-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell to download a file and display the file content.</span></span>

### <a name="the-powershell-sample"></a><span data-ttu-id="1acc5-261">L'esempio di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1acc5-261">The PowerShell sample</span></span>
    # Prepare an Azure SQL database to be used by the Sqoop tutorial

    #region - provide the following values

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription to access the server.
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
    Write-Host "Creating the log4jlogs table and the mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create the log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create the mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating the HDInsight cluster and the dependent services ..." -ForegroundColor Green

    # Create the default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create the HDInsight cluster
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

    # Validate the cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process the source file

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define the connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing the source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from the source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into the destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process the source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove the "java.lang.Exception" from the first element of the array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList to remove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove the lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write to the destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from the cluster to the SQL database

    Write-Host "Preprocessing the source file ..." -ForegroundColor Green

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
