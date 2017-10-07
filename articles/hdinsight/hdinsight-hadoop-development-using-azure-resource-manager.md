---
title: strumenti di aaaMigrate tooAzure Gestione risorse per HDInsight | Documenti Microsoft
description: "Modalità di strumenti toomigrate tooAzure lo sviluppo di gestione risorse per i cluster HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Strumenti di sviluppo basato su Gestione risorse tooAzure la migrazione per i cluster HDInsight

In HDInsight stanno per essere deprecati gli strumenti basati su Azure Service Management (ASM) per HDInsight. Se è stato utilizzato hello HDInsight .NET SDK toowork, CLI di Azure o Azure PowerShell con i cluster HDInsight, sono invitati toouse hello basato su Azure Resource Manager ARM le versioni di .NET SDK in futuro, PowerShell e CLI. In questo articolo vengono forniti i puntatori sull'approccio toomigrate toohello nuovo basato su ARM. Se applicabile, questo articolo sono inoltre disponibili le differenze di hello tra gli approcci ASM e ARM hello per HDInsight.

> [!IMPORTANT]
> supporto di Hello per ASM basati CLI, PowerShell e .NET SDK verrà sospeso **il 1 ° gennaio 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Migrazione tooAzure CLI di Azure Resource Manager
Hello CLI di Azure predefinito ora tooAzure modalità di gestione risorse (ARM), a meno che non si esegue l'aggiornamento da un'installazione precedente. In questo caso, potrebbe essere necessario toouse hello `azure config mode arm` modalità tooARM tooswitch dei comandi.

comandi di base Hello che hello CLI di Azure fornito toowork con HDInsight mediante la gestione del servizio di Azure (ASM) sono hello stesso quando si utilizza ARM; tuttavia alcuni parametri e le opzioni siano i nuovi nomi, e sono disponibili molti nuovi parametri quando si utilizza ARM. Ad esempio, è ora possibile usare `azure hdinsight cluster create` toospecify hello rete virtuale di Azure che deve essere creato un cluster o Hive e Oozie metastore informazioni.

Ecco i comandi di base per l'utilizzo di HDInsight tramite Azure Resource Manager:

* `azure hdinsight cluster create` : crea un nuovo cluster HDInsight.
* `azure hdinsight cluster delete` : elimina un cluster HDInsight esistente.
* `azure hdinsight cluster show` : visualizza informazioni su un cluster esistente.
* `azure hdinsight cluster list` : elenca i cluster HDInsight per la sottoscrizione di Azure

Hello utilizzare `-h` passare parametri di hello tooinspect e le opzioni disponibili per ogni comando.

### <a name="new-commands"></a>Nuovi comandi
Ecco i nuovi comandi disponibili con Azure Resource Manager:

* `azure hdinsight cluster resize`-dinamicamente modifiche hello numero di nodi di lavoro in cluster hello
* `azure hdinsight cluster enable-http-access`-Abilita HTTPs accesso toohello cluster (in per impostazione predefinita)
* `azure hdinsight cluster disable-http-access`-Disabilita cluster toohello di accesso HTTPs
* `azure hdinsight script-action`: fornisce i comandi per la creazione o la gestione di azioni script in un cluster.
* `azure hdinsight config`-sono disponibili comandi per la creazione di un file di configurazione che può essere utilizzata con hello `hdinsight cluster create` comando tooprovide informazioni di configurazione.

### <a name="deprecated-commands"></a>Comandi deprecati
Se si utilizza hello `azure hdinsight job` cluster di HDInsight tooyour processi toosubmit comandi, queste non sono disponibili tramite i comandi di hello ARM. Se è necessario tooprogrammatically invia i processi tooHDInsight dagli script, si dovrebbe usare invece hello API REST fornita da HDInsight. Per ulteriori informazioni sull'invio di processi usando le API REST, vedere hello seguenti documenti.

* [Eseguire processi MapReduce con Hadoop in HDInsight mediante cURL](hdinsight-hadoop-use-mapreduce-curl.md)
* [Eseguire query Hive con Hadoop in HDInsight mediante Curl](hdinsight-hadoop-use-hive-curl.md)
* [Eseguire processi Pig con Hadoop in HDInsight mediante cUrl](hdinsight-hadoop-use-pig-curl.md)

Per informazioni su altri toorun modi MapReduce, Hive, Pig in modo interattivo, vedere [utilizzare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md), [utilizzare Hive con Hadoop in HDInsight](hdinsight-use-hive.md), e [usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>esempi
**Creazione di un cluster**

* Comando precedente (ASM): `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Nuovo comando (ARM): `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Eliminazione di un cluster**

* Comando precedente (ASM): `azure hdinsight cluster delete myhdicluster`
* Nuovo comando (ARM): `azure hdinsight cluster delete mycluster -g myresourcegroup`

**Elencare i cluster**

* Comando precedente (ASM): `azure hdinsight cluster list`
* Nuovo comando (ARM): `azure hdinsight cluster list`

> [!NOTE]
> Per il comando di elenco hello, specificando hello gruppo di risorse utilizzando `-g` restituirà solo i cluster hello nel gruppo di risorse specificato hello.
> 
> 

**Mostrare informazioni sul cluster**

* Comando precedente (ASM): `azure hdinsight cluster show myhdicluster`
* Nuovo comando (ARM): `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>La migrazione di Azure PowerShell tooAzure Gestione risorse
informazioni generali su Azure PowerShell Hello in modalità Azure Resource Manager (ARM) hello sono reperibile in [tramite Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

i cmdlet di Azure PowerShell ARM Hello può essere installato side-by-side con hello cmdlet ASM. è possibile distinguere i cmdlet di Hello dalle due modalità di hello con i relativi nomi.  modalità ARM Hello è *AzureRmHDInsight* nei nomi di cmdlet hello confronto troppo*AzureHDInsight* in modalità ASM hello.  Ad esempio, *New-AzureRmHDInsightCluster* e *New-AzureHDInsightCluster*. Parametri e le opzioni possono avere nomi nuovi e sono disponibili molti nuovi parametri quando si usa ARM.  Ad esempio, alcuni cmdlet richiedono una nuova opzione denominata *- ResourceGroupName*. 

Prima di poter utilizzare i cmdlet di HDInsight hello, è necessario connettersi tooyour account Azure e creare un nuovo gruppo di risorse:

* Login-AzureRmAccount o [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). Vedere [Autenticazione di un'entità servizio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Cmdlet rinominati
hello toolist i cmdlet di HDInsight ASM nella console di Windows PowerShell:

    help *azurermhdinsight*

Hello nella tabella seguente elenca i cmdlet ASM hello e i relativi nomi in modalità ARM hello:

| Cmdlet ASM | Cmdlet ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Nuovi cmdlet
di seguito Hello sono hello nuovi cmdlet che sono disponibili solo in modalità di hello ARM. 

**Cmdlet correlati all'azione script:**

* **Get-AzureRmHDInsightPersistedScriptAction**: hello Ottiene persistente azioni script per un cluster sono elencati in ordine cronologico e ottiene i dettagli per un'azione script persistente specificato. 
* **Get-AzureRmHDInsightScriptActionHistory**: Ottiene cronologia dell'azione script hello per un cluster e sono elencati in ordine cronologico inverso o ottiene i dettagli di un'azione di script eseguita in precedenza. 
* **Remove AzureRmHDInsightPersistedScriptAction**: rimuove un'azione script persistente da un cluster HDInsight.
* **Set-AzureRmHDInsightPersistedScriptAction**: imposta una toobe azione script precedentemente eseguito un'azione di script con salvataggio permanente.
* **AzureRmHDInsightScriptAction inviare**: invia un nuovo cluster di Azure HDInsight tooan azione script. 

Per altre informazioni sull'utilizzo, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).

**Cmdlet correlati a identità del cluster:**

* **AzureRmHDInsightClusterIdentity aggiungere**: aggiunge un oggetto di configurazione di cluster identità tooa cluster in modo che hello cluster HDInsight possono accedere gli archivi di Azure Data Lake. Vedere [Creare un cluster HDInsight con Archivio Data Lake tramite Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>esempi
**Creare cluster**

Comando precedente (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Nuovo comando (ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Eliminare cluster**

Comando precedente (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Nuovo comando (ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Elencare cluster**

Comando precedente (ASM):

    Get-AzureHDInsightCluster

Nuovo comando (ARM):

    Get-AzureRmHDInsightCluster 

**Mostrare cluster**

Comando precedente (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Nuovo comando (ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Altri esempi
* [Creare cluster HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Invio di processi Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Eseguire processi Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md)
* [Eseguire processi Sqoop con Azure PowerShell per Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Migrazione toohello basato su ARM HDInsight .NET SDK
Hello basate su gestione dei servizi Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) è obsoleta. Si consiglia toouse hello basate su Gestione risorse di Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx). Hello pacchetti basato su ASM HDInsight seguenti sono deprecati.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

In questa sezione fornisce i puntatori toomore informazioni su come tooperform determinate attività utilizzando hello SDK basato su ARM.

| Come... utilizzando hello basato su ARM SDK HDInsight | Collegamenti |
| --- | --- |
| Creare cluster HDInsight con .NET SDK |Vedere [Creare cluster basati su Linux in HDInsight tramite .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| Personalizzare un cluster tramite un'azione script con .NET SDK |Vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| Autenticare le applicazioni in modo interattivo tramite Azure Active Directory con .NET SDK |Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md) frammento di codice Hello in questo articolo usa l'approccio interattivo autenticazione hello. |
| Autenticare le applicazioni in modo non interattivo tramite Azure Active Directory con .NET SDK |Vedere [Creare applicazioni .NET HDInsight di autenticazione non interattiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| Inviare un processo Hive con .NET SDK |Vedere [Eseguire query Hive con HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| Inviare un processo Pig con .NET SDK |Vedere [Eseguire processi Pig con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| Inviare un processo Sqoop con .NET SDK |Vedere [Eseguire processi Sqoop con .NET SDK per Hadoop in HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| Elencare cluster HDInsight con .NET SDK |Vedere la sezione su come elencare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| Ridimensionare cluster HDInsight con .NET SDK |Vedere la sezione su come ridimensionare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Concedere o revocare l'accesso tooHDInsight cluster mediante .NET SDK |Vedere [cluster tooHDInsight di concedere o revocare l'accesso](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Aggiornare le credenziali utente HTTP per i cluster HDInsight con .NET SDK |Vedere la sezione su come aggiornare le credenziali utente HTTP in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| Trovare l'account di archiviazione predefinito hello per i cluster HDInsight mediante .NET SDK |Vedere [trovare account di archiviazione di hello predefinito per i cluster HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Eliminare cluster HDInsight con .NET SDK |Vedere la sezione su come eliminare cluster in [Gestire cluster Hadoop in HDInsight tramite .NET SDK](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>esempi
Di seguito sono riportati alcuni esempi su come un'operazione viene eseguita utilizzando hello basato su ASM SDK e il frammento di codice equivalente hello per hello SDK basato su ARM.

**Creazione di un client CRUD del cluster**

* Comando precedente (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Nuovo comando (ARM) (autorizzazione dell'entità servizio)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Nuovo comando (ARM) (autorizzazione utente)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Creazione di un cluster**

* Comando precedente (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Nuovo comando (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Abilitazione dell'accesso HTTP**

* Comando precedente (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Nuovo comando (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Eliminazione di un cluster**

* Comando precedente (ASM)
  
        client.DeleteCluster(dnsName);
* Nuovo comando (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

