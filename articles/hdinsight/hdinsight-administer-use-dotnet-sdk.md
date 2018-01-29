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
ms.date: 12/15/2017
ms.author: jgao
ms.openlocfilehash: d881d47e26460d3fff89c01245bba4c608dc8b08
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Gestire cluster Hadoop in HDInsight tramite .NET SDK
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Ecco come gestire cluster HDInsight usando [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Prerequisiti**

Per eseguire le procedure descritte nell'articolo è necessario:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-to-azure-hdinsight"></a>Connettersi ad Azure HDInsight

Sono necessari i pacchetti NuGet seguenti:

```
Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
Install-Package Microsoft.Azure.Management.ResourceManager -Pre
Install-Package Microsoft.Azure.Management.HDInsight
```

L'esempio di codice indica come connettersi ad Azure prima di poter amministrare cluster HDInsight con una sottoscrizione Azure.

```csharp
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
```

Quando si esegue questo programma verrà visualizzato un prompt dei comandi.  Per non visualizzare il prompt dei comandi, vedere [Creare applicazioni .NET HDInsight di autenticazione non interattive](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Creare i cluster
Vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Elencare cluster
Il frammento di codice seguente elenca i cluster e alcune proprietà:

```csharp
var results = _hdiManagementClient.Clusters.List();
foreach (var name in results.Clusters) {
    Console.WriteLine("Cluster Name: " + name.Name);
    Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
    Console.WriteLine("\t Cluster location: " + name.Location);
    Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
}
```

## <a name="delete-clusters"></a>Eliminare cluster
Per eliminare un cluster in modo sincrono o asincrono, usare il frammento di codice seguente: 

```csharp
_hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
_hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");
```

## <a name="scale-clusters"></a>Ridimensionare i cluster
La funzionalità di scalabilità del cluster consente di modificare il numero di nodi del ruolo di lavoro usati da un cluster in esecuzione in Azure HDInsight senza dover ricreare il cluster.

> [!NOTE]
> Sono supportati solo i cluster con HDInsight versione 3.1.3 o successive. Se non si è certi della versione del cluster, è possibile controllare la pagina delle proprietà.  Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

Questa sezione descrive l'impatto della modifica del numero di nodi dati per ogni tipo di cluster supportato da HDInsight:

* Hadoop
  
    È possibile aumentare facilmente il numero di nodi del ruolo di lavoro in un cluster Hadoop in esecuzione senza conseguenze per eventuali processi in sospeso o in esecuzione. È inoltre possibile inviare nuovi processi mentre è in corso l'operazione. Gli errori in un'operazione di scalabilità vengono gestiti in modo che il cluster rimanga sempre in uno stato funzionale.
  
    Quando un cluster Hadoop viene ridimensionato riducendo il numero di nodi dati, alcuni dei servizi del cluster vengono riavviati. In questo modo, tutti i processi in esecuzione e in attesa daranno esito negativo dopo il completamento dell'operazione di ridimensionamento. È tuttavia possibile inviare nuovamente i processi una volta completata l'operazione.
* hbase
  
    È possibile aggiungere o rimuovere facilmente nodi nel cluster HBase mentre è in esecuzione. I server a livello di area vengono bilanciati automaticamente entro pochi minuti dal completamento dell'operazione di ridimensionamento. È tuttavia possibile anche bilanciare manualmente i server a livello di area accedendo al nodo head del cluster ed eseguendo i comandi seguenti da una finestra del prompt dei comandi:
  
    ```bash
    >pushd %HBASE_HOME%\bin
    >hbase shell
    >balancer
    ```
* Storm
  
    È possibile aggiungere o rimuovere facilmente nodi dati dal cluster Storm mentre è in esecuzione. Tuttavia, dopo il completamento dell'operazione di ridimensionamento, è necessario bilanciare nuovamente la topologia.
  
    A tale scopo, è possibile scegliere tra due opzioni:
  
  * Interfaccia utente Web di Storm
  * Interfaccia della riga di comando (CLI)
    
    Per altre informazioni, fare riferimento alla [documentazione su Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) .
    
    L'interfaccia utente Web di Storm è disponibile nel cluster HDInsight:
    
    ![Ribilanciamento di HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Di seguito viene fornito un esempio d'uso del comando CLI per ribilanciare la topologia di Storm:
    
    ```cli
    ## Reconfigure the topology "mytopology" to use 5 worker processes,
    ## the spout "blue-spout" to use 3 executors, and
    ## the bolt "yellow-bolt" to use 10 executors
    $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10
    ```

Il frammento di codice seguente indica come ridimensionare un cluster in modo sincrono o asincrono:

```csharp
_hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
_hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   
```

## <a name="grantrevoke-access"></a>Concedere/Revocare l'accesso
Per i cluster HDInsight sono disponibili i servizi Web HTTP seguenti (tutti con endpoint RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Per impostazione predefinita, a questi servizi è concesso l'accesso. L'accesso può essere revocato/concesso, Per revocare:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = false,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

Per concedere:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = enable,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

> [!NOTE]
> La concessione/revoca dell'accesso implica la reimpostazione del nome utente e della password del cluster.
> 
> 

Questa operazione può essere eseguita anche tramite il portale. Vedere l'articolo su come [amministrare HDInsight con il portale di Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Aggiornare le credenziali utente HTTP
È la stessa procedura di [Concedere/revocare l'accesso HTTP](#grant/revoke-access). Se al cluster è stato concesso l'accesso HTTP, è necessario prima revocarlo.  E quindi concedere l'accesso con le nuove credenziali utente HTTP.

## <a name="find-the-default-storage-account"></a>Trovare l'account di archiviazione predefinito
Il frammento di codice seguente dimostra come ottenere il nome dell’account di archiviazione predefinito e la chiave dell’account di archiviazione predefinita per un cluster.

```csharp
var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
foreach (var key in results.Configuration.Keys)
{
    Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
}
```

## <a name="submit-jobs"></a>Inviare i processi
**Inviare processi MapReduce**

Vedere [Eseguire gli esempi di Hadoop in HDInsight](hadoop/apache-hadoop-run-samples-linux.md).

**Inviare processi Hive** 

Vedere [Eseguire query Hive con HDInsight .NET SDK](hadoop/apache-hadoop-use-hive-dotnet-sdk.md)

**Inviare processi Pig**

Vedere [Esecuzione di processi Pig con .NET SDK per Hadoop in HDInsight](hadoop/apache-hadoop-use-pig-dotnet-sdk.md)

**Inviare processi Sqoop**

Vedere [Usare Sqoop con Hadoop in HDInsight](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md).

**Inviare processi Oozie**

Vedere [Usare Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-to-azure-blob-storage"></a>Caricare dati nell'archivio BLOB di Azure
Vedere[Caricare dati in HDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Vedere anche
* [Documentazione di riferimento su HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)
* [Amministrare HDInsight con il portale di Azure][hdinsight-admin-portal]
* [Amministrare HDInsight con l'interfaccia della riga di comando][hdinsight-admin-cli]
* [Creare cluster HDInsight][hdinsight-provision]
* [Caricare dati in HDInsight][hdinsight-upload-data]
* [Introduzione ad Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]:hadoop/submit-apache-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-mapreduce]:hadoop/hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


