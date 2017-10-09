---
title: aaaCustomize cluster HDInsight tramite script azioni - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize mediante l'azione di Script.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Personalizzare cluster HDInsight basati su Windows tramite Azione script
**Azione di script** può essere utilizzato tooinvoke [script personalizzati](hdinsight-hadoop-script-actions.md) durante il processo di creazione di cluster hello per l'installazione di software aggiuntivi in un cluster.

informazioni di Hello in questo articolo sono di tipo cluster HDInsight basati su tooWindows specifici. Per i cluster basati su Linux, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Cluster HDInsight possono essere personalizzati in una vasta gamma di altri modi, ad esempio l'utilizzo di altri account di archiviazione di Azure, la modifica hello Hadoop file di configurazione (hive-Site.XML Core-Site.XML, e così via) o aggiunta di raccolte (ad esempio, Hive e Oozie) condivise in percorsi comuni in cluster hello. Queste personalizzazioni possono essere eseguite tramite Azure PowerShell, hello Azure HDInsight .NET SDK o hello portale di Azure. Per altre informazioni, vedere [Creare cluster Hadoop basati su Windows in HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Genera script azione nel processo di creazione di cluster hello
Genera script azione viene utilizzato solo durante un cluster è in corso di hello corso di creazione. Hello diagramma seguente illustra quando viene eseguita l'azione di Script durante il processo di creazione di hello:

![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]

Durante l'esecuzione di script hello, cluster hello immette hello **ClusterCustomization** fase. In questa fase, hello script viene eseguito con l'account amministratore di sistema hello, in parallelo in tutte hello specificato nodi cluster hello e fornisce i privilegi di amministratore completi nei nodi hello.

> [!NOTE]
> Poiché si dispone dei privilegi di amministratore nei nodi del cluster hello durante il **ClusterCustomization** fase, è possibile utilizzare le operazioni di tooperform script hello come arrestare e avviare servizi, inclusi quelli correlati Hadoop. Pertanto, come parte dello script hello, è necessario assicurarsi che i servizi Ambari hello e altri servizi correlati a Hadoop siano in esecuzione prima di script hello al termine dell'esecuzione. Questi servizi sono necessari toosuccessfully verificare hello integrità e dello stato del cluster hello durante la creazione. Se si modifica qualsiasi configurazione in cluster che influisce su questi servizi, è necessario utilizzare funzioni di supporto hello forniti. Per altre informazioni sulle funzioni di supporto, vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].
>
>

output di Hello e di log degli errori di hello per script hello vengono archiviati nell'account di archiviazione predefinito hello specificato per il cluster hello. Hello i log vengono archiviati in una tabella con nome hello **u < \cluster-name-fragment >< \time-stamp > setuplog**. Questi sono registri di aggregazione da eseguire in tutti i nodi di hello (nodo head e i nodi di lavoro) cluster hello uno script di hello.

Ogni cluster possono accettare più azioni di script che vengono richiamate nell'ordine di hello in cui sono state specificate. Uno script può essere eseguito nel nodo head hello, nodi di lavoro hello o entrambi.

HDInsight offre diversi hello tooinstall di script seguenti componenti nei cluster HDInsight:

| Nome | Script |
| --- | --- |
| **Installare Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Vedere [Installare e usare Spark in cluster Hadoop di HDInsight][hdinsight-install-spark]. |
| **Installare R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Vedere [Installare e usare R nei cluster HDInsight][hdinsight-install-r]. |
| **Installare Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Installare Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install.md). |
| **Precaricare le librerie Hive** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Script di chiamata utilizzando hello portale di Azure
**Dal portale di Azure hello**

1. Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. Nella sezione Configurazione facoltativi per hello **azioni Script** pannello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:

    ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize azione Script Usa un cluster")

    <table border='1'>
        <tr><th>Proprietà</th><th>Valore</th></tr>
        <tr><td>Nome</td>
            <td>Specificare un nome per l'azione script hello.</td></tr>
        <tr><td>URI script</td>
            <td>Specificare hello URI toohello script che è richiamato toocustomize hello cluster. s</td></tr>
        <tr><td>Head/Lavoro</td>
            <td>Specificare i nodi di hello (**Head** o **lavoro**) in cui personalizzazione hello script viene eseguito.</b>.
        <tr><td>parameters</td>
            <td>Specificare i parametri di hello, se richiesti dallo script hello.</td></tr>
    </table>

    Premere INVIO tooadd più di uno script azione tooinstall più componenti cluster hello.
3. Fare clic su **selezionare** toosave hello configurazione script dell'azione e continuare con la creazione del cluster.

## <a name="call-scripts-using-azure-powershell"></a>Chiamare script con Azure PowerShell
Questo script di PowerShell seguente viene illustrato come tooinstall Spark in Windows basato su cluster HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall altro software, sono necessari file di script hello tooreplace nello script hello:

Quando richiesto, immettere le credenziali di hello per cluster hello. Può richiedere alcuni minuti prima che venga creato il cluster hello.

## <a name="call-scripts-using-net-sdk"></a>Chiamare script con .NET SDK
Hello seguente esempio viene illustrato come tooinstall Spark in Windows basato su cluster HDInsight. tooinstall altro software, sono necessari file di script hello tooreplace nel codice hello.

**un cluster di HDInsight con Spark toocreate**

1. Creare un'applicazione console C# in Visual Studio.
2. Dalla Console di gestione pacchetti Nuget hello, eseguire hello comando seguente.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Dopo l'utilizzo di istruzioni nel file Program.cs hello hello di utilizzo:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Inserire codice hello nella classe hello con seguenti hello:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
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
5. Premere **F5** toorun un'applicazione hello.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Supporto per software open source usato nei cluster HDInsight
servizio Microsoft Azure HDInsight Hello è una piattaforma flessibile che consente applicazioni big data toobuild nel cloud hello utilizzando un ecosistema di tecnologie open source in corrispondenza di Hadoop. Microsoft Azure offre un livello di supporto generale per le tecnologie open source, come descritto in hello **supportano ambito** sezione di hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">sito Web di domande frequenti su Azure supporta</a>. servizio HDInsight Hello fornisce un ulteriore livello di supporto per alcuni dei componenti di hello, come descritto di seguito.

Esistono due tipi di componenti open source che sono disponibili nel servizio HDInsight hello:

* **I componenti predefiniti** -questi componenti sono pre-installati nei cluster HDInsight e forniscono funzionalità di base del cluster di hello. Ad esempio, ResourceManager YARN, linguaggio di query Hive hello (HiveQL) e libreria Mahout hello appartenere toothis categoria. È disponibile in un elenco completo dei componenti cluster [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md) </a>.
* **I componenti personalizzati** -, come un utente del cluster di hello, puoi installare o utilizzare nel carico di lavoro qualsiasi componente disponibile nella community hello o creato dall'utente.

I componenti predefiniti sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati e il supporto Microsoft verrà Guida tooisolate e risolvere i problemi correlati toothese componenti.
>
> I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Ciò potrebbe comportare la risoluzione problema hello o chiedere che tooengage i canali disponibili per hello apertura di tecnologie di origine in cui si trova esperienza completa per tale tecnologia. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Per i progetti Apache sono anche disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/) e [Spark](http://spark.apache.org/).
>
>

servizio HDInsight Hello modi diversi componenti personalizzati toouse. Indipendentemente dalla modalità un componente viene utilizzato o installato nel cluster hello, hello stesso livello di supporto si applica. Di seguito è riportato un elenco dei modi più comuni di hello componenti personalizzati possono essere utilizzati nei cluster HDInsight:

1. Invio di processi - Hadoop o altri tipi di processi che utilizzano componenti personalizzati di esecuzione può essere inviato toohello cluster.
2. Personalizzazione del cluster - durante la creazione del cluster, è possibile specificare impostazioni aggiuntive e i componenti personalizzati che verranno installati nei nodi del cluster hello.
3. Esempi - per componenti personalizzati più diffusi, Microsoft e altri utenti possono fornire esempi di come utilizzare questi componenti nei cluster di HDInsight hello. Questi esempi vengono forniti senza supporto.

## <a name="develop-script-action-scripts"></a>Sviluppare script di Azione di script
Vedere [Sviluppare script di Azione script per HDInsight][hdinsight-write-script].

## <a name="see-also"></a>Vedere anche
* [Creare i cluster Hadoop in HDInsight] [ hdinsight-provision-cluster] vengono fornite istruzioni su come toocreate un HDInsight cluster tramite altre opzioni personalizzate.
* [Sviluppare script di Azione script per HDInsight][hdinsight-write-script]
* [Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]
* [Installare e usare R nei cluster HDInsight][hdinsight-install-r]
* [Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).
* [Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"
