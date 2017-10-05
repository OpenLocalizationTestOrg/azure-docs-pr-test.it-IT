---
title: Gestire cluster Hadoop in HDInsight con .NET SDK - Azure | Microsoft Docs
description: "Informazioni su come eseguire attività amministrative per i cluster Hadoop in HDInsight tramite HDInsight .NET SDK."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="64ea9-103">Gestire cluster Hadoop in HDInsight tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="64ea9-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="64ea9-104">Ecco come gestire cluster HDInsight usando [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="64ea9-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="64ea9-105">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="64ea9-105">**Prerequisites**</span></span>

<span data-ttu-id="64ea9-106">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="64ea9-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="64ea9-107">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="64ea9-107">**An Azure subscription**.</span></span> <span data-ttu-id="64ea9-108">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="64ea9-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="64ea9-109">Connettersi ad Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="64ea9-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="64ea9-110">Sono necessari i pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="64ea9-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="64ea9-111">L'esempio di codice indica come connettersi ad Azure prima di poter amministrare cluster HDInsight con una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="64ea9-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
            {
                var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
                var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                    ClientId, 
                    new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                    PromptBehavior.Always, 
                    UserIdentifier.AnyUser);
                return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
            }
            /// <summary>
            /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
            /// </summary>
            /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
            /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
            /// <param name="authToken">An authentication token for your Azure subscription</param>
            static void EnableHDInsight(TokenCloudCredentials authToken)
            {
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="64ea9-112">Quando si esegue questo programma verrà visualizzato un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="64ea9-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="64ea9-113">Per non visualizzare il prompt dei comandi, vedere [Creare applicazioni .NET HDInsight di autenticazione non interattive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="64ea9-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="64ea9-114">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="64ea9-114">Create clusters</span></span>
<span data-ttu-id="64ea9-115">Vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="64ea9-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="64ea9-116">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="64ea9-116">List clusters</span></span>
<span data-ttu-id="64ea9-117">Il frammento di codice seguente elenca i cluster e alcune proprietà:</span><span class="sxs-lookup"><span data-stu-id="64ea9-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="64ea9-118">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="64ea9-118">Delete clusters</span></span>
<span data-ttu-id="64ea9-119">Per eliminare un cluster in modo sincrono o asincrono, usare il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="64ea9-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="64ea9-120">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="64ea9-120">Scale clusters</span></span>
<span data-ttu-id="64ea9-121">La funzionalità di scalabilità del cluster consente di modificare il numero di nodi del ruolo di lavoro usati da un cluster in esecuzione in Azure HDInsight senza dover ricreare il cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea9-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="64ea9-122">Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive.</span><span class="sxs-lookup"><span data-stu-id="64ea9-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="64ea9-123">Se non si è certi della versione del cluster, è possibile controllare la pagina delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="64ea9-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="64ea9-124">Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="64ea9-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="64ea9-125">Questa sezione descrive l'impatto della modifica del numero di nodi dati per ogni tipo di cluster supportato da HDInsight:</span><span class="sxs-lookup"><span data-stu-id="64ea9-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="64ea9-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="64ea9-126">Hadoop</span></span>
  
    <span data-ttu-id="64ea9-127">È possibile aumentare facilmente il numero di nodi del ruolo di lavoro in un cluster Hadoop in esecuzione senza conseguenze per eventuali processi in sospeso o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="64ea9-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="64ea9-128">È inoltre possibile inviare nuovi processi mentre è in corso l'operazione.</span><span class="sxs-lookup"><span data-stu-id="64ea9-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="64ea9-129">Gli errori in un'operazione di scalabilità vengono gestiti in modo che il cluster rimanga sempre in uno stato funzionale.</span><span class="sxs-lookup"><span data-stu-id="64ea9-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="64ea9-130">Quando un cluster Hadoop viene ridimensionato riducendo il numero di nodi dati, alcuni dei servizi del cluster vengono riavviati.</span><span class="sxs-lookup"><span data-stu-id="64ea9-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="64ea9-131">In questo modo, tutti i processi in esecuzione e in attesa daranno esito negativo dopo il completamento dell'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="64ea9-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="64ea9-132">È tuttavia possibile inviare nuovamente i processi una volta completata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="64ea9-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="64ea9-133">HBase</span><span class="sxs-lookup"><span data-stu-id="64ea9-133">HBase</span></span>
  
    <span data-ttu-id="64ea9-134">È possibile aggiungere o rimuovere facilmente nodi nel cluster HBase mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="64ea9-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="64ea9-135">I server a livello di area vengono bilanciati automaticamente entro pochi minuti dal completamento dell'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="64ea9-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="64ea9-136">È tuttavia possibile anche bilanciare manualmente i server a livello di area accedendo al nodo head del cluster ed eseguendo i comandi seguenti da una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="64ea9-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="64ea9-137">Storm</span><span class="sxs-lookup"><span data-stu-id="64ea9-137">Storm</span></span>
  
    <span data-ttu-id="64ea9-138">È possibile aggiungere o rimuovere facilmente nodi dati dal cluster Storm mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="64ea9-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="64ea9-139">Tuttavia, dopo il completamento dell'operazione di ridimensionamento, è necessario bilanciare nuovamente la topologia.</span><span class="sxs-lookup"><span data-stu-id="64ea9-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="64ea9-140">A tale scopo, è possibile scegliere tra due opzioni:</span><span class="sxs-lookup"><span data-stu-id="64ea9-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="64ea9-141">Interfaccia utente Web di Storm</span><span class="sxs-lookup"><span data-stu-id="64ea9-141">Storm web UI</span></span>
  * <span data-ttu-id="64ea9-142">Interfaccia della riga di comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="64ea9-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="64ea9-143">Per altre informazioni, fare riferimento alla [documentazione su Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .</span><span class="sxs-lookup"><span data-stu-id="64ea9-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="64ea9-144">L'interfaccia utente Web di Storm è disponibile nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="64ea9-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![Ribilanciamento di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="64ea9-146">Di seguito viene fornito un esempio d'uso del comando CLI per ribilanciare la topologia di Storm:</span><span class="sxs-lookup"><span data-stu-id="64ea9-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="64ea9-147">Il frammento di codice seguente indica come ridimensionare un cluster in modo sincrono o asincrono:</span><span class="sxs-lookup"><span data-stu-id="64ea9-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="64ea9-148">Concedere/Revocare l'accesso</span><span class="sxs-lookup"><span data-stu-id="64ea9-148">Grant/revoke access</span></span>
<span data-ttu-id="64ea9-149">Per i cluster HDInsight sono disponibili i servizi Web HTTP seguenti (tutti con endpoint RESTful):</span><span class="sxs-lookup"><span data-stu-id="64ea9-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="64ea9-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="64ea9-150">ODBC</span></span>
* <span data-ttu-id="64ea9-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="64ea9-151">JDBC</span></span>
* <span data-ttu-id="64ea9-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="64ea9-152">Ambari</span></span>
* <span data-ttu-id="64ea9-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="64ea9-153">Oozie</span></span>
* <span data-ttu-id="64ea9-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="64ea9-154">Templeton</span></span>

<span data-ttu-id="64ea9-155">Per impostazione predefinita, a questi servizi è concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="64ea9-155">By default, these services are granted for access.</span></span> <span data-ttu-id="64ea9-156">L'accesso può essere revocato/concesso,</span><span class="sxs-lookup"><span data-stu-id="64ea9-156">You can revoke/grant the access.</span></span> <span data-ttu-id="64ea9-157">Per revocare:</span><span class="sxs-lookup"><span data-stu-id="64ea9-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="64ea9-158">Per concedere:</span><span class="sxs-lookup"><span data-stu-id="64ea9-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="64ea9-159">La concessione/revoca dell'accesso implica la reimpostazione del nome utente e della password del cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea9-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="64ea9-160">Questa operazione può essere eseguita anche tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="64ea9-160">This can also be done via the Portal.</span></span> <span data-ttu-id="64ea9-161">Vedere l'articolo su come [amministrare HDInsight con il portale di Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="64ea9-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="64ea9-162">Aggiornare le credenziali utente HTTP</span><span class="sxs-lookup"><span data-stu-id="64ea9-162">Update HTTP user credentials</span></span>
<span data-ttu-id="64ea9-163">È la stessa procedura di [Concedere/revocare l'accesso HTTP](#grant/revoke-access). Se al cluster è stato concesso l'accesso HTTP, è necessario prima revocarlo.</span><span class="sxs-lookup"><span data-stu-id="64ea9-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="64ea9-164">E quindi concedere l'accesso con le nuove credenziali utente HTTP.</span><span class="sxs-lookup"><span data-stu-id="64ea9-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="64ea9-165">Trovare l'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="64ea9-165">Find the default storage account</span></span>
<span data-ttu-id="64ea9-166">Il frammento di codice seguente dimostra come ottenere il nome dell’account di archiviazione predefinito e la chiave dell’account di archiviazione predefinita per un cluster.</span><span class="sxs-lookup"><span data-stu-id="64ea9-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="64ea9-167">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="64ea9-167">Submit jobs</span></span>
<span data-ttu-id="64ea9-168">**Inviare processi MapReduce**</span><span class="sxs-lookup"><span data-stu-id="64ea9-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="64ea9-169">Vedere [Eseguire gli esempi di Hadoop in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="64ea9-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="64ea9-170">**Inviare processi Hive**</span><span class="sxs-lookup"><span data-stu-id="64ea9-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="64ea9-171">Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="64ea9-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="64ea9-172">**Inviare processi Pig**</span><span class="sxs-lookup"><span data-stu-id="64ea9-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="64ea9-173">Vedere [Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="64ea9-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="64ea9-174">**Inviare processi Sqoop**</span><span class="sxs-lookup"><span data-stu-id="64ea9-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="64ea9-175">Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="64ea9-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="64ea9-176">**Inviare processi Oozie**</span><span class="sxs-lookup"><span data-stu-id="64ea9-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="64ea9-177">Vedere [Usare Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="64ea9-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="64ea9-178">Caricare dati nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="64ea9-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="64ea9-179">Vedere[Caricare dati in HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="64ea9-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="64ea9-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="64ea9-180">See Also</span></span>
* [<span data-ttu-id="64ea9-181">Documentazione di riferimento su HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="64ea9-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="64ea9-182">[Amministrare HDInsight con il portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="64ea9-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="64ea9-183">[Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="64ea9-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="64ea9-184">[Creare cluster HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="64ea9-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="64ea9-185">[Caricare dati in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="64ea9-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="64ea9-186">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="64ea9-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


