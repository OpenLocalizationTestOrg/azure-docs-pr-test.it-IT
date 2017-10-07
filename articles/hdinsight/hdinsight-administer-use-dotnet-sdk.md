---
title: cluster aaaManage Hadoop in HDInsight mediante .NET SDK - Azure | Documenti Microsoft
description: "Informazioni su come attività amministrative tooperform per hello cluster Hadoop in HDInsight mediante HDInsight .NET SDK."
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
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="99fd9-103">Gestire cluster Hadoop in HDInsight tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="99fd9-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="99fd9-104">Informazioni su come cluster di HDInsight toomanage tramite [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="99fd9-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="99fd9-105">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="99fd9-105">**Prerequisites**</span></span>

<span data-ttu-id="99fd9-106">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="99fd9-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="99fd9-107">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="99fd9-107">**An Azure subscription**.</span></span> <span data-ttu-id="99fd9-108">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="99fd9-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="99fd9-109">Connettersi tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="99fd9-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="99fd9-110">È necessario hello pacchetti Nuget seguenti:</span><span class="sxs-lookup"><span data-stu-id="99fd9-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="99fd9-111">Hello nell'esempio di codice seguente mostra come cluster di tooconnect tooAzure prima di poter amministrare HDInsight nella sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="99fd9-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
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
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="99fd9-112">Quando si esegue questo programma verrà visualizzato un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="99fd9-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="99fd9-113">Se non si desidera prompt hello toosee, vedere [creare applicazioni di HDInsight .NET di autenticazione non interattivo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="99fd9-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="99fd9-114">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="99fd9-114">Create clusters</span></span>
<span data-ttu-id="99fd9-115">Vedere [basati su Linux creare cluster HDInsight con hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="99fd9-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="99fd9-116">Elencare cluster</span><span class="sxs-lookup"><span data-stu-id="99fd9-116">List clusters</span></span>
<span data-ttu-id="99fd9-117">Hello frammento di codice seguente sono elencate alcune proprietà e i cluster:</span><span class="sxs-lookup"><span data-stu-id="99fd9-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="99fd9-118">Eliminare cluster</span><span class="sxs-lookup"><span data-stu-id="99fd9-118">Delete clusters</span></span>
<span data-ttu-id="99fd9-119">Utilizzare hello seguente frammento di codice toodelete un cluster in modo sincrono o asincrono:</span><span class="sxs-lookup"><span data-stu-id="99fd9-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="99fd9-120">Ridimensionare i cluster</span><span class="sxs-lookup"><span data-stu-id="99fd9-120">Scale clusters</span></span>
<span data-ttu-id="99fd9-121">scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="99fd9-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="99fd9-122">Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive.</span><span class="sxs-lookup"><span data-stu-id="99fd9-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="99fd9-123">Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="99fd9-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="99fd9-124">Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="99fd9-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="99fd9-125">impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:</span><span class="sxs-lookup"><span data-stu-id="99fd9-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="99fd9-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="99fd9-126">Hadoop</span></span>
  
    <span data-ttu-id="99fd9-127">È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="99fd9-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="99fd9-128">È inoltre possibile avviare nuovi processi mentre è in corso hello operazione.</span><span class="sxs-lookup"><span data-stu-id="99fd9-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="99fd9-129">Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.</span><span class="sxs-lookup"><span data-stu-id="99fd9-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="99fd9-130">Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati.</span><span class="sxs-lookup"><span data-stu-id="99fd9-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="99fd9-131">In questo modo tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="99fd9-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="99fd9-132">È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="99fd9-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="99fd9-133">HBase</span><span class="sxs-lookup"><span data-stu-id="99fd9-133">HBase</span></span>
  
    <span data-ttu-id="99fd9-134">Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="99fd9-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="99fd9-135">Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello.</span><span class="sxs-lookup"><span data-stu-id="99fd9-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="99fd9-136">Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo al nodo head hello del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="99fd9-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="99fd9-137">Storm</span><span class="sxs-lookup"><span data-stu-id="99fd9-137">Storm</span></span>
  
    <span data-ttu-id="99fd9-138">Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="99fd9-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="99fd9-139">Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="99fd9-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="99fd9-140">A tale scopo, è possibile scegliere tra due opzioni:</span><span class="sxs-lookup"><span data-stu-id="99fd9-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="99fd9-141">Interfaccia utente Web di Storm</span><span class="sxs-lookup"><span data-stu-id="99fd9-141">Storm web UI</span></span>
  * <span data-ttu-id="99fd9-142">Interfaccia della riga di comando (CLI)</span><span class="sxs-lookup"><span data-stu-id="99fd9-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="99fd9-143">Consultare toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="99fd9-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="99fd9-144">interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="99fd9-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![Ribilanciamento di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="99fd9-146">Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:</span><span class="sxs-lookup"><span data-stu-id="99fd9-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="99fd9-147">Hello seguente frammento di codice viene illustrato come tooresize un cluster in modo sincrono o asincrono:</span><span class="sxs-lookup"><span data-stu-id="99fd9-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="99fd9-148">Concedere/Revocare l'accesso</span><span class="sxs-lookup"><span data-stu-id="99fd9-148">Grant/revoke access</span></span>
<span data-ttu-id="99fd9-149">Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:</span><span class="sxs-lookup"><span data-stu-id="99fd9-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="99fd9-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="99fd9-150">ODBC</span></span>
* <span data-ttu-id="99fd9-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="99fd9-151">JDBC</span></span>
* <span data-ttu-id="99fd9-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="99fd9-152">Ambari</span></span>
* <span data-ttu-id="99fd9-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="99fd9-153">Oozie</span></span>
* <span data-ttu-id="99fd9-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="99fd9-154">Templeton</span></span>

<span data-ttu-id="99fd9-155">Per impostazione predefinita, a questi servizi è concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="99fd9-155">By default, these services are granted for access.</span></span> <span data-ttu-id="99fd9-156">È possibile revocare o concedere l'accesso hello.</span><span class="sxs-lookup"><span data-stu-id="99fd9-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="99fd9-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="99fd9-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="99fd9-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="99fd9-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="99fd9-159">Per concedere o revocare l'accesso hello, sarà necessario reimpostare la password e nome utente di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="99fd9-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="99fd9-160">Questa operazione può anche essere eseguita tramite hello portale.</span><span class="sxs-lookup"><span data-stu-id="99fd9-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="99fd9-161">Vedere [HDInsight amministrare tramite hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="99fd9-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="99fd9-162">Aggiornare le credenziali utente HTTP</span><span class="sxs-lookup"><span data-stu-id="99fd9-162">Update HTTP user credentials</span></span>
<span data-ttu-id="99fd9-163">È hello stessa stored procedure come [accesso Grant/revoke HTTP](#grant/revoke-access). Se il cluster hello è stata concessa hello accesso HTTP, è necessario revocare.</span><span class="sxs-lookup"><span data-stu-id="99fd9-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="99fd9-164">E quindi concedere l'accesso di hello con nuove credenziali utente HTTP.</span><span class="sxs-lookup"><span data-stu-id="99fd9-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="99fd9-165">Trovare l'account di archiviazione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="99fd9-165">Find hello default storage account</span></span>
<span data-ttu-id="99fd9-166">Hello seguente frammento di codice viene illustrato come tooget hello Nome account di archiviazione predefinito e hello chiave account di archiviazione predefinito per un cluster.</span><span class="sxs-lookup"><span data-stu-id="99fd9-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="99fd9-167">Inviare i processi</span><span class="sxs-lookup"><span data-stu-id="99fd9-167">Submit jobs</span></span>
<span data-ttu-id="99fd9-168">**processi MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="99fd9-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="99fd9-169">Vedere [Eseguire gli esempi di Hadoop in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="99fd9-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="99fd9-170">**processi Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="99fd9-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="99fd9-171">Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="99fd9-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="99fd9-172">**processi Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="99fd9-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="99fd9-173">Vedere [Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="99fd9-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="99fd9-174">**toosubmit Sqoop processi**</span><span class="sxs-lookup"><span data-stu-id="99fd9-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="99fd9-175">Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="99fd9-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="99fd9-176">**processi di Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="99fd9-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="99fd9-177">Vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="99fd9-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="99fd9-178">Carica l'archiviazione Blob di dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="99fd9-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="99fd9-179">Vedere [caricare dati tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="99fd9-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="99fd9-180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="99fd9-180">See Also</span></span>
* [<span data-ttu-id="99fd9-181">Documentazione di riferimento su HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="99fd9-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="99fd9-182">[Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="99fd9-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="99fd9-183">[Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="99fd9-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="99fd9-184">[Creare cluster HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="99fd9-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="99fd9-185">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="99fd9-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="99fd9-186">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="99fd9-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


