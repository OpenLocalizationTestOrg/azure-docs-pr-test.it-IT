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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gestire cluster Hadoop in HDInsight tramite .NET SDK
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Informazioni su come cluster di HDInsight toomanage tramite [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Prerequisiti**

Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Connettersi tooAzure HDInsight

È necessario hello pacchetti Nuget seguenti:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Hello nell'esempio di codice seguente mostra come cluster di tooconnect tooAzure prima di poter amministrare HDInsight nella sottoscrizione Azure.

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

Quando si esegue questo programma verrà visualizzato un prompt dei comandi.  Se non si desidera prompt hello toosee, vedere [creare applicazioni di HDInsight .NET di autenticazione non interattivo](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Creare i cluster
Vedere [basati su Linux creare cluster HDInsight con hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Elencare cluster
Hello frammento di codice seguente sono elencate alcune proprietà e i cluster:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Eliminare cluster
Utilizzare hello seguente frammento di codice toodelete un cluster in modo sincrono o asincrono: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Ridimensionare i cluster
scalabilità funzionalità cluster di Hello consente numero hello toochange di nodi di lavoro utilizzato da un cluster che è in esecuzione in Azure HDInsight senza toore-creare cluster hello.

> [!NOTE]
> Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive. Se si è certi della versione di hello del cluster, è possibile controllare una pagina delle proprietà hello.  Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

impatto di Hello di modifica del numero di hello di nodi di dati per ogni tipo di cluster supportato da HDInsight:

* Hadoop
  
    È possibile aumentare facilmente numero hello di nodi di lavoro in un cluster Hadoop che è in esecuzione senza conseguenze per tutti i processi in sospeso o in esecuzione. È inoltre possibile avviare nuovi processi mentre è in corso hello operazione. Gli errori in un'operazione di ridimensionamento normalmente vengono gestiti in modo che hello cluster rimanga sempre in uno stato funzionale.
  
    Quando un cluster Hadoop è ridotta, riducendo il numero di hello di nodi di dati, alcuni dei servizi di hello cluster hello vengono riavviati. In questo modo tutti in esecuzione e in sospeso toofail processi al completamento di hello di hello l'operazione di ridimensionamento. È tuttavia possibile inviare di nuovo i processi di hello al termine dell'operazione di hello.
* HBase
  
    Senza problemi, è possibile aggiungere o rimuovere cluster HBase di nodi tooyour mentre è in esecuzione. Server locali sono bilanciati automaticamente entro pochi minuti di completare l'operazione di ridimensionamento hello. Tuttavia, è possibile bilanciare manualmente server regionali hello accedendo al nodo head hello del cluster e in esecuzione hello seguendo i comandi da una finestra del prompt dei comandi:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Senza problemi, è possibile aggiungere o rimuovere cluster Storm tooyour nodi di dati in fase di esecuzione. Tuttavia, dopo il completamento dell'operazione di ridimensionamento hello, sarà necessario topologia hello toorebalance.
  
    A tale scopo, è possibile scegliere tra due opzioni:
  
  * Interfaccia utente Web di Storm
  * Interfaccia della riga di comando (CLI)
    
    Consultare toohello [documentazione di Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) per altri dettagli.
    
    interfaccia utente web di Storm Hello è disponibile nel cluster HDInsight hello:
    
    ![Ribilanciamento di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Di seguito è riportato un esempio come toouse hello CLI comando topologia di Storm toorebalance hello:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Hello seguente frammento di codice viene illustrato come tooresize un cluster in modo sincrono o asincrono:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Concedere/Revocare l'accesso
Cluster HDInsight sono hello (tutti questi servizi hanno endpoint REST) i servizi HTTP web seguente:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Per impostazione predefinita, a questi servizi è concesso l'accesso. È possibile revocare o concedere l'accesso hello. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Per concedere o revocare l'accesso hello, sarà necessario reimpostare la password e nome utente di hello del cluster.
> 
> 

Questa operazione può anche essere eseguita tramite hello portale. Vedere [HDInsight amministrare tramite hello Azure portal][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Aggiornare le credenziali utente HTTP
È hello stessa stored procedure come [accesso Grant/revoke HTTP](#grant/revoke-access). Se il cluster hello è stata concessa hello accesso HTTP, è necessario revocare.  E quindi concedere l'accesso di hello con nuove credenziali utente HTTP.

## <a name="find-hello-default-storage-account"></a>Trovare l'account di archiviazione predefinito hello
Hello seguente frammento di codice viene illustrato come tooget hello Nome account di archiviazione predefinito e hello chiave account di archiviazione predefinito per un cluster.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Inviare i processi
**processi MapReduce toosubmit**

Vedere [Eseguire gli esempi di Hadoop in HDInsight](hdinsight-hadoop-run-samples-linux.md).

**processi Hive toosubmit** 

Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)

**processi Pig toosubmit**

Vedere [Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)

**toosubmit Sqoop processi**

Vedere [Usare Sqoop con Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**processi di Oozie toosubmit**

Vedere [utilizzare Oozie con Hadoop toodefine ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Carica l'archiviazione Blob di dati tooAzure
Vedere [caricare dati tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Vedere anche
* [Documentazione di riferimento su HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)
* [Amministrazione di HDInsight tramite hello portale di Azure][hdinsight-admin-portal]
* [Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]
* [Creare cluster HDInsight][hdinsight-provision]
* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Introduzione ad Azure HDInsight][hdinsight-get-started]

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


