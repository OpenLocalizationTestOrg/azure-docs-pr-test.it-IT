---
title: cluster di HDInsight aaaCustomize usando le azioni script - Azure | Documenti Microsoft
description: "Aggiungere i componenti personalizzati che basati su tooLinux HDInsight cluster usando le azioni di Script. Le azioni script sono script Bash che è possibile configurazione del cluster utilizzati toocustomize hello o aggiungere altri servizi e le utilità come tonalità, Solr o R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Personalizzare cluster HDInsight basati su Linux tramite Azione script

HDInsight fornisce un'opzione di configurazione denominata **genera Script azione** che richiama script personalizzati che consentono di personalizzare cluster hello. Questi script vengono utilizzati tooinstall i componenti aggiuntivi e modificare le impostazioni di configurazione. Le azioni script possono essere utilizzate durante o dopo la creazione del cluster.

> [!IMPORTANT]
> azioni di Hello possibilità toouse script in un cluster già in esecuzione è disponibile solo per i cluster HDInsight basati su Linux.
>
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Le azioni script possono anche essere pubblicata toohello Azure Marketplace come un'applicazione di HDInsight. Alcuni degli esempi di hello in questo documento Mostra come installare un'applicazione di HDInsight utilizzando i comandi di azione di script di PowerShell e hello .NET SDK. Per ulteriori informazioni sulle applicazioni di HDInsight, vedere [HDInsight pubblicare applicazioni in Azure Marketplace hello](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Autorizzazioni

Se si utilizza un cluster di HDInsight appartenenti a un dominio, sono disponibili due Ambari le autorizzazioni necessarie quando si utilizzano le azioni script con cluster hello:

* **AMBARI. ESEGUIRE\_personalizzato\_comando**: il ruolo di amministratore Ambari hello dispone dell'autorizzazione per impostazione predefinita.
* **CLUSTER. ESEGUIRE\_personalizzato\_comando**: entrambi hello amministrazione Cluster HDInsight e Ambari amministratore dispongono di questa autorizzazione per impostazione predefinita.

Per altre informazioni sull'uso delle autorizzazioni con HDInsight aggiunto a un dominio, vedere [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire cluster HDInsight aggiunti al dominio).

## <a name="access-control"></a>Controllo di accesso

Se non si è amministratore hello/proprietario della sottoscrizione Azure, l'account deve disporre almeno **collaboratore** gruppo di risorse toohello di accesso che contiene il cluster di HDInsight hello.

Inoltre, se si sta creando un cluster HDInsight, un utente con almeno **collaboratore** toohello accesso sottoscrizione di Azure deve registrato in precedenza provider hello per HDInsight. Registrazione del provider si verifica quando un utente con sottoscrizione di collaboratore accesso toohello crea una risorsa per hello prima sottoscrizione hello. Può essere eseguita anche senza creare una risorsa [registrando un provider tramite REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Per ulteriori informazioni sull'utilizzo di gestione degli accessi, vedere hello seguenti documenti:

* [Introduzione alla gestione di accesso nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md)
* [Utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Informazioni sulle azioni script

Un'azione script è semplicemente uno script Bash a cui si forniscono parametri e un URI. script di Hello viene eseguito in nodi di cluster di HDInsight hello. di seguito Hello sono caratteristiche e funzionalità delle azioni di scripting.

* Devono essere archiviati in un URI che sia accessibile dal cluster HDInsight hello. di seguito Hello sono possibili percorsi di archiviazione:

    * Un **archivio Azure Data Lake** account che sia accessibile dal cluster HDInsight hello. Per informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store usando il portale](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Quando si utilizza uno script archiviato nell'archivio Data Lake, il formato dell'URI hello è `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hello servizio principale HDInsight utilizza tooaccess archivio Data Lake deve avere accesso in lettura toohello script.

    * Un blob in un **account di archiviazione Azure** che è uno di questi account di archiviazione primario o altre hello per il cluster HDInsight hello. HDInsight è concesso l'accesso tooboth di questi tipi di account di archiviazione durante la creazione del cluster.

    * Un servizio di condivisione file pubblico, ad esempio BLOB di Azure, GitHub, OneDrive, Dropbox e così via.

        Ad esempio URI, vedere hello [script azione script di esempio](#example-script-action-scripts) sezione.

        > [!WARNING]
        > HDInsight supporta solo account di archiviazione di Azure __per uso generico__. Non supporta attualmente hello __nell'archiviazione Blob__ tipo di account.

* Può essere limitata troppo**eseguiti solo alcuni tipi di nodi**, ad esempio head nodi o di lavoro.

  > [!NOTE]
  > Se utilizzato con HDInsight Premium, è possibile specificare che devono essere utilizzati script di hello sul nodo del bordo hello.

* Possono essere **persistenti** o **ad hoc**.

    **Persistente** gli script sono cluster toohello aggiunta di nodi tooworker applicato dopo l'esecuzione di script hello. Ad esempio, la scalabilità del cluster di hello.

    Uno script persistente potrebbe anche applicare tipo di nodo tooanother modifiche, ad esempio un nodo head.

  > [!IMPORTANT]
  > Le azioni script persistenti devono avere un nome univoco.

    Gli script **ad hoc** non sono persistenti. Non sono cluster toohello aggiunta di nodi tooworker applicato dopo script hello è stato eseguito. Successivamente è possibile alzare di livello un tooa script ad hoc persistente script o abbassare di livello uno script di script con salvataggio permanente tooan ad hoc.

  > [!IMPORTANT]
  > Le azioni script usate durante la creazione di un cluster vengono automaticamente rese persistenti.
  >
  > Gli script che hanno esito negativo non vengono resi persistenti, anche in presenza di indicazioni specifiche in tal senso.

* Può accettare **parametri** utilizzati dallo script hello durante l'esecuzione.
* Eseguire con **privilegi al livello radice** nei nodi del cluster hello.
* Può essere utilizzato tramite hello **portale di Azure**, **Azure PowerShell**, **CLI di Azure**, o **HDInsight .NET SDK**

cluster Hello mantiene una cronologia di tutti gli script sono stati eseguiti. cronologia Hello è utile quando è necessario toofind hello ID di uno script per le operazioni di innalzamento o abbassamento di livello.

> [!IMPORTANT]
> Non è tooundo alcun metodo automatico hello le modifiche apportate da un'azione di script. È possibile annullare manualmente le modifiche di hello oppure fornire uno script che li inverte.


### <a name="script-action-in-hello-cluster-creation-process"></a>Genera script azione nel processo di creazione di cluster hello

Le azioni script usate durante la creazione del cluster sono leggermente diverse da quelle eseguite in un cluster esistente:

* script Hello è **automaticamente persistente**.
* Oggetto **errore** in hello script può causare hello cluster creazione processo toofail.

Hello diagramma seguente illustra quando viene eseguita l'azione di Script durante il processo di creazione di hello:

![Personalizzazione di cluster HDInsight e fasi durante la creazione di un cluster][img-hdi-cluster-states]

script di Hello viene eseguito quando viene configurato HDInsight. In questa fase, viene eseguito lo script hello in parallelo in tutte hello i nodi specificati nel cluster hello e viene eseguito con privilegi radice nodi hello.

> [!NOTE]
> Poiché nei nodi del cluster hello, script di hello viene eseguito con privilegi di livello radice, è possibile eseguire operazioni come l'arresto e avvio di servizi, inclusi i servizi correlati a Hadoop. Se si arresta i servizi, è necessario assicurarsi che il servizio di Ambari hello e altri servizi correlati a Hadoop siano in esecuzione prima di script hello al termine dell'esecuzione. Questi servizi sono necessari toosuccessfully determinare hello integrità e dello stato del cluster hello durante la creazione.


Durante la creazione del cluster, è possibile usare più azioni di script alla volta. Questi script vengono richiamati nell'ordine di hello in cui sono stati specificati.

> [!IMPORTANT]
> Le azioni di script devono essere completate entro 60 minuti; in caso contrario si verifica un timeout. Durante il provisioning del cluster, script di hello viene eseguito contemporaneamente ad altri processi di installazione e configurazione. Contesa per le risorse, ad esempio larghezza di banda della CPU ora o di rete potrebbe essere hello script tootake più toofinish rispetto a quello usato nell'ambiente di sviluppo.
>
> hello toominimize tempo accetta toorun hello script, evitare di attività, ad esempio il download e la compilazione di applicazioni dall'origine. Precompilazione di applicazioni e archiviare file binario hello in archiviazione di Azure.


### <a name="script-action-on-a-running-cluster"></a>Azione script in un cluster in esecuzione

A differenza degli script azioni utilizzate durante la creazione del cluster, un errore in uno script eseguite su un cluster già in esecuzione non determina automaticamente lo stato di hello cluster toochange tooa non riuscita. Al termine del processo di uno script, cluster hello deve restituire lo stato "running" tooa.

> [!IMPORTANT]
> Anche se il cluster hello presenta uno stato 'in esecuzione', hello script non riuscito potrebbe essere interrotto operazioni. Ad esempio, uno script è stato possibile eliminare i file necessari per il cluster hello.
>
> Le azioni di script eseguite con privilegi di radice, pertanto è necessario assicurarsi di comprendere cosa uno script prima di applicarla tooyour cluster.

Quando l'applicazione di un cluster di tooa script, lo stato del cluster hello cambia toofrom **esecuzione** troppo**accettato**, quindi **HDInsight configurazione**e infine di nuovo troppo**Esecuzione** per gli script ha esito positivo. stato dello script Hello viene registrato nella cronologia dell'azione script hello ed è possibile utilizzare questo toodetermine informazioni script hello è riuscita o meno. Ad esempio, hello `Get-AzureRmHDInsightScriptActionHistory` cmdlet di PowerShell può essere utilizzato tooview hello stato di uno script. Restituisce toohello di informazioni simili seguente testo:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Se è stata modificata la password utente (amministrazione) di hello cluster dopo la creazione del cluster hello, script azioni è state eseguite su questo cluster potrebbe non riuscire. Se si dispone di eventuali azioni script persistenti di nodi di lavoro di destinazione, questi script potrebbero non riuscire quando si aumenta il cluster hello.

## <a name="example-script-action-scripts"></a>Script di Azione script di esempio

Script delle azioni di script può essere utilizzato tramite hello utilità seguenti:

* Portale di Azure
* Azure PowerShell
* Interfaccia della riga di comando di Azure
* HDInsight .NET SDK

HDInsight fornisce hello tooinstall gli script seguenti componenti nei cluster HDInsight:

| Nome | Script |
| --- | --- |
| **Aggiungere un account di archiviazione di Azure** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Vedere [cluster HDInsight di aggiungere ulteriore spazio di archiviazione tooan](hdinsight-hadoop-add-storage.md). |
| **Installare Hue.** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Vedere [Installare e usare Hue in cluster HDInsight](hdinsight-hadoop-hue-linux.md). |
| **Installare Presto** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Vedere [Installare e usare Presto nei cluster HDInsight Hadoop](hdinsight-hadoop-install-presto.md). |
| **Installare Solr** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install-linux.md). |
| **Installare Giraph** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install-linux.md). |
| **Precaricare le librerie Hive** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Vedere l'articolo relativo all' [aggiunta di librerie Hive in cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Installare o aggiornare Mono** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. Vedere [Installare o aggiornare Mono in HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Usare un'azione script durante la creazione di un cluster

In questa sezione vengono forniti esempi in modi diversi di hello che è possibile usare azioni script durante la creazione di un cluster HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Utilizzare un'azione di Script durante la creazione del cluster da hello portale di Azure

1. Avviare la creazione di un cluster come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Fermarsi quando si raggiunge hello __riepilogo Cluster__ sezione.

2. Da hello __riepilogo Cluster__ sezione, seleziona hello __modifica__ dei collegamenti per __impostazioni avanzate__.

    ![Collegamento impostazioni avanzate](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Da hello __impostazioni avanzate__ selezionare __Script azioni__. Da hello __Script azioni__ selezionare __+ nuovo invio__

    ![Inviare una nuova azione script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Hello utilizzare __selezionare uno script__ tooselect voce uno script di pre-effettuato. toouse uno script personalizzato, selezionare __personalizzato__ e quindi fornire hello __nome__ e __l'URI dello script Bash__ per lo script.

    ![Aggiungere uno script nel modulo di script selezionare hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello nella tabella seguente vengono descritti gli elementi di hello in form di hello:

    | Proprietà | Valore |
    | --- | --- |
    | Selezionare uno script | toouse lo script, seleziona __personalizzato__. In caso contrario, selezionare uno degli script hello fornito. |
    | Nome |Specificare un nome per l'azione script hello. |
    | URI script Bash |Specificare hello URI toohello script che è richiamato toocustomize hello cluster. |
    | Head/Worker/Zookeeper |Specificare i nodi di hello (**Head**, **lavoro**, o **ZooKeeper**) in cui personalizzazione hello viene eseguito uno script. |
    | parameters |Specificare i parametri di hello, se richiesti dallo script hello. |

    Hello utilizzare __mantenere questa azione script__ tooensure voce che hello script viene applicato durante le operazioni di ridimensionamento.

5. Selezionare __crea__ script hello toosave. È quindi possibile utilizzare __+ invia di nuovo__ tooadd un altro script.

    ![Azioni script multiple](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Una volta aggiunta di script, utilizzare hello __selezionare__ pulsante e quindi hello __Avanti__ pulsante tooreturn toohello __riepilogo Cluster__ sezione.

3. cluster di hello toocreate, selezionare __crea__ da hello __riepilogo Cluster__ selezione.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Usare Azione di script dai modelli di Gestione risorse di Azure

esempi di Hello in questa sezione illustrano come toouse script azioni con modelli di gestione risorse di Azure.

#### <a name="before-you-begin"></a>Prima di iniziare

* Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight Powershell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).
* Per istruzioni su come toocreate modelli, vedere [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Se Azure PowerShell non è stato usato in precedenza con Gestione risorse, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Creare cluster usando l'azione script

1. Copiare hello seguente percorso tooa modelli nel computer in uso. Questo modello consente di installare Giraph in hello headnodes e lavoro i nodi del cluster di hello. È inoltre possibile verificare se il modello JSON hello è valido. Incollare il contenuto del modello in [JSONLint](http://jsonlint.com/), uno strumento di convalida JSON disponibile online.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Avviare PowerShell di Azure e accedere tooyour account Azure. Dopo aver fornito le credenziali, hello comando restituisce le informazioni relative all'account.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Se si dispone di più sottoscrizioni, fornire l'ID sottoscrizione hello desiderato toouse per la distribuzione.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > È possibile utilizzare `Get-AzureRmSubscription` tooget un elenco di tutte le sottoscrizioni associate all'account, che include l'ID sottoscrizione hello per ognuno di essi.

4. Se non è già disponibile un gruppo di risorse, crearne uno. Specificare il nome di hello del gruppo di risorse hello e il percorso che è necessario per la soluzione. Viene restituito un riepilogo del nuovo gruppo di risorse hello.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. una distribuzione per il gruppo di risorse, eseguire hello toocreate **New AzureRmResourceGroupDeployment** comando e specificare i parametri necessari hello. i parametri di Hello includono hello dati seguenti:

    * Nome per la distribuzione
    * nome di Hello del gruppo di risorse
    * percorso di Hello o modello di URL toohello creato.

  Passare anche gli eventuali altri parametri richiesti dal modello. In questo caso, hello script azione tooinstall R nel cluster hello non richiede alcun parametro.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Sono valori tooprovide richiesta per i parametri di hello definiti nel modello di hello.

1. Quando il gruppo di risorse hello è stato distribuito, viene visualizzato un riepilogo della distribuzione hello.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Se la distribuzione non riesce, è possibile utilizzare i seguenti cmdlet tooget informazioni sugli errori di hello hello.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Usare un'azione script durante la creazione di un cluster da Azure PowerShell

In questa sezione, utilizziamo hello [Aggiungi AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke script utilizzando l'azione Script toocustomize un cluster. Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell. Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).

Hello script riportato di seguito viene illustrato come tooapply un'azione di script durante la creazione di un cluster con PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Può richiedere alcuni minuti prima che venga creato il cluster hello.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Utilizzare un'azione di Script durante la creazione del cluster da hello HDInsight .NET SDK

Hello HDInsight .NET SDK fornisce librerie client che rende più semplice toowork con HDInsight da un'applicazione .NET. Per un esempio di codice, vedere [basati su Linux creare cluster HDInsight con hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Applicare un tooa genera Script azione in esecuzione del cluster

In questa sezione, informazioni su come tooapply script tooa azioni in esecuzione del cluster.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Applicare un tooa genera Script azione in esecuzione del cluster da hello portale di Azure

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight.

2. Panoramica del cluster HDInsight hello, selezionare hello **azioni Script** riquadro.

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > È inoltre possibile selezionare **tutte le impostazioni** e quindi selezionare **azioni Script** da hello sezione Impostazioni.

3. Dall'alto hello di hello sezione azioni Script, selezionare **invia di nuovo**.

    ![Aggiungere un tooa di script in esecuzione del cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Hello utilizzare __selezionare uno script__ tooselect voce uno script di pre-effettuato. toouse uno script personalizzato, selezionare __personalizzato__ e quindi fornire hello __nome__ e __l'URI dello script Bash__ per lo script.

    ![Aggiungere uno script nel modulo di script selezionare hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Hello nella tabella seguente vengono descritti gli elementi di hello in form di hello:

    | Proprietà | Valore |
    | --- | --- |
    | Selezionare uno script | toouse lo script, seleziona __personalizzato__. In caso contrario, selezionare uno degli script disponibili. |
    | Nome |Specificare un nome per l'azione script hello. |
    | URI script Bash |Specificare hello URI toohello script che è richiamato toocustomize hello cluster. |
    | Head/Worker/Zookeeper |Specificare i nodi di hello (**Head**, **lavoro**, o **ZooKeeper**) in cui personalizzazione hello viene eseguito uno script. |
    | parameters |Specificare i parametri di hello, se richiesti dallo script hello. |

    Hello utilizzare __mantenere questa azione script__ voce toomake che hello script viene applicato durante le operazioni di ridimensionamento.

5. Infine, utilizzare hello **crea** cluster toohello di pulsante tooapply hello script.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Applicare un tooa genera Script azione in esecuzione i cluster di Azure PowerShell

Prima di procedere, assicurarsi di aver installato e configurato Azure PowerShell. Per informazioni sulla configurazione di un toorun workstation, i cmdlet HDInsight PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).

Hello esempio seguente viene illustrato come un cluster in esecuzione di script azione tooa tooapply:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Al termine dell'operazione di hello, viene visualizzato toohello di informazioni simili seguente testo:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Applicare un tooa genera Script azione in esecuzione del cluster da hello CLI di Azure

Prima di procedere, assicurarsi di avere installato e configurato hello CLI di Azure. Per ulteriori informazioni, vedere [installazione hello Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure modalità di gestione delle risorse, utilizzare hello comando hello riga di comando seguente:

        azure config mode arm

2. Utilizzare hello seguente tooauthenticate tooyour sottoscrizione di Azure.

        azure login

3. Utilizzare hello successivo comando tooapply un tooa azione script in esecuzione del cluster

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Se non vengono specificati alcuni parametri per il comando, verrà richiesto di specificarli. Se hello script specificare con `-u` accetta parametri, è possibile specificare tali utilizzando hello `-p` parametro.

    I tipi di nodo validi sono `headnode`, `workernode`, e `zookeeper`. Se script hello devono essere tipi di nodo toomultiple applicato, specificare i tipi di hello separati da un ';'. ad esempio `-n headnode;workernode`.

    toopersist hello script, aggiungere hello `--persistOnSuccess`. È inoltre possibile mantenere in un secondo momento script hello utilizzando `azure hdinsight script-action persisted set`.

    Al termine del processo di hello, viene visualizzato toohello simili di output il testo seguente:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Applicare un tooa genera Script azione in esecuzione tramite l'API REST di cluster

Vedere l'articolo su come [eseguire azioni script in un cluster in esecuzione](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Applicare un tooa genera Script azione in esecuzione del cluster da hello HDInsight .NET SDK

Per un esempio di utilizzo di hello .NET SDK tooapply script tooa cluster, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Visualizzare la cronologia, alzare e abbassare di livello le azioni script

### <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure

1. Da hello [portale di Azure](https://portal.azure.com), selezionare il cluster HDInsight.

2. Panoramica del cluster HDInsight hello, selezionare hello **azioni Script** riquadro.

    ![Riquadro Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > È inoltre possibile selezionare **tutte le impostazioni** e quindi selezionare **azioni Script** da hello sezione Impostazioni.

4. Una cronologia degli script per il cluster viene visualizzata nella sezione azioni Script hello. Queste informazioni includono un elenco degli script persistenti. Nella schermata di hello riportata di seguito, è possibile visualizzare tale hello Solr script è stato eseguito nel cluster. schermata di Hello non sono presenti eventuali script persistenti.

    ![Sezione Azioni script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Selezione di uno script dalla cronologia hello Visualizza sezione proprietà hello per questo script. Dall'alto hello della schermata di hello, è possibile eseguire di nuovo script hello o alzare di livello.

    ![Proprietà delle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. È inoltre possibile utilizzare hello **...**  toohello a destra delle voci sulle azioni di tooperform sezione azioni Script hello.

    ![Uso di ... nelle azioni script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Uso di Azure PowerShell

| Utilizzare la seguente hello... | Anche... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Recuperare informazioni sulle azioni script persistenti |
| Get-AzureRmHDInsightScriptActionHistory |Recuperare una cronologia dei cluster toohello applicare azioni di script o i dettagli per uno script specifico |
| Set-AzureRmHDInsightPersistedScriptAction |Alza di livello un ad hoc tooa azioni script persistenti genera script azione |
| Remove-AzureRmHDInsightPersistedScriptAction |Abbassa di livello un'azione di script con salvataggio permanente azione tooan ad hoc |

> [!IMPORTANT]
> Utilizzando `Remove-AzureRmHDInsightPersistedScriptAction` non vengono annullate le azioni di hello eseguite da uno script. Questo cmdlet rimuove solo flag persistente hello.

Hello lo script di esempio seguente viene illustrato come utilizzare toopromote cmdlet hello e abbassare di livello uno script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Utilizzo di hello CLI di Azure

| Utilizzare la seguente hello... | Anche... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Recuperare un elenco di azioni script con salvataggio permanente |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Recuperare informazioni su una specifica azione script con salvataggio permanente |
| `azure hdinsight script-action history list <clustername>` |Recuperare una cronologia dei cluster toohello applicare azioni di script |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Recuperare informazioni su un'azione script specifica |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Alza di livello un ad hoc tooa azioni script persistenti genera script azione |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Abbassa di livello un'azione di script con salvataggio permanente azione tooan ad hoc |

> [!IMPORTANT]
> Utilizzando `azure hdinsight script-action persisted delete` non vengono annullate le azioni di hello eseguite da uno script. Questo cmdlet rimuove solo flag persistente hello.

### <a name="using-hello-hdinsight-net-sdk"></a>Utilizzo di hello HDInsight .NET SDK

Per un esempio dell'utilizzo di cronologia di hello .NET SDK tooretrieve script da un cluster, alzare di livello o abbassare di livello gli script, vedere [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Questo esempio viene illustrato come un'applicazione di HDInsight mediante tooinstall hello .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Supporto per software open source usato nei cluster HDInsight

servizio Microsoft Azure HDInsight Hello utilizza un ecosistema di tecnologie open source in corrispondenza di Hadoop. Microsoft Azure offre un livello di supporto generale per le tecnologie open source. Per ulteriori informazioni, vedere hello **ambito supporto** sezione di hello [sito Web di Azure Support FAQ](https://azure.microsoft.com/support/faq/). servizio HDInsight Hello fornisce un ulteriore livello di supporto per i componenti predefiniti.

Esistono due tipi di componenti open source che sono disponibili nel servizio HDInsight hello:

* **I componenti predefiniti** -questi componenti sono pre-installati nei cluster HDInsight e forniscono funzionalità di base del cluster di hello. Ad esempio, ResourceManager YARN, linguaggio di query Hive hello (HiveQL) e libreria Mahout hello appartenere toothis categoria. È disponibile in un elenco completo dei componenti cluster [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight](hdinsight-component-versioning.md).
* **I componenti personalizzati** -, come un utente del cluster di hello, puoi installare o utilizzare nel carico di lavoro qualsiasi componente disponibile nella community hello o creato dall'utente.

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati. Il supporto di Microsoft consente tooisolate e risolvere i problemi correlati toothese componenti.
>
> I componenti personalizzati ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Supporto tecnico Microsoft potrebbe essere in grado di tooresolve problema di hello o si potrebbero chiedere i canali disponibili tooengage per tecnologie open source hello in cui si trova esperienza completa per tale tecnologia. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).

servizio HDInsight Hello modi diversi componenti personalizzati toouse. Hello si applica allo stesso livello di supporto, indipendentemente da come un componente viene utilizzato o installato nel cluster hello. Hello elenco seguente vengono descritti modi più comuni di hello che i componenti personalizzati possono essere utilizzati nei cluster HDInsight:

1. Invio di processi - Hadoop o altri tipi di processi che utilizzano componenti personalizzati di esecuzione può essere inviato toohello cluster.

2. Personalizzazione del cluster - durante la creazione del cluster, è possibile specificare impostazioni aggiuntive e i componenti personalizzati che vengono installati nei nodi del cluster hello.

3. Esempi - per componenti personalizzati più diffusi, Microsoft e altri utenti possono fornire esempi di come utilizzare questi componenti nei cluster di HDInsight hello. Questi esempi vengono forniti senza supporto.

## <a name="troubleshooting"></a>Risoluzione dei problemi

È possibile utilizzare Ambari web UI tooview informazioni registrate dalle azioni di script. Se lo script hello non riesce durante la creazione del cluster, sono disponibili nell'account di archiviazione predefinito hello associato hello cluster anche hello log. In questa sezione vengono fornite informazioni sul funzionamento dei registri tooretrieve hello utilizzando entrambe queste opzioni.

### <a name="using-hello-ambari-web-ui"></a>Utilizzo dell'interfaccia utente Web Ambari hello

1. Nel browser passare toohttps://CLUSTERNAME.azurehdinsight.net. Sostituire CLUSTERNAME con nome hello del cluster HDInsight.

    Quando richiesto, immettere nome dell'account admin hello (amministratore) e la password per il cluster hello. Credenziali di amministratore hello tooreenter potrebbe essere in un web form.

2. Selezionare hello hello barra nella parte superiore di hello della pagina hello **ops** voce. Viene visualizzato un elenco delle operazioni correnti e precedenti eseguite su cluster hello tramite Ambari.

    ![Barra nell'interfaccia utente di Ambari con selezionato ops](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Trovare le voci di hello associate **eseguire\_customscriptaction** in hello **operazioni** colonna. Queste voci vengono create quando esegue le azioni Script hello.

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    hello tooview STDOUT e STDERR uscita, selezionare una voce run\customscriptaction hello e drill-down tramite collegamenti hello. Questo output viene generato quando l'esecuzione dello script hello e possono contenere informazioni utili.

### <a name="access-logs-from-hello-default-storage-account"></a>Registri di accesso dall'account di archiviazione predefinito hello

Se la creazione del cluster di hello non riesce a causa di errore script tooa, hello registri sono accessibili dall'account di archiviazione cluster hello.

* Hello i log di archiviazione sono disponibili in `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Schermata delle operazioni](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    In questa directory, hello registri sono organizzati per nodo head, workernode e nodi zookeeper separatamente. Di seguito sono riportati alcuni esempi:

    * **Nodo head** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Nodo del ruolo di lavoro** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Nodo Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Tutti i stdout e stderr dell'host corrispondente hello è caricato toohello account di archiviazione. Per ogni azione script esiste un file **output-\*.txt** e un file **errors-\*.txt**. file txt di output di Hello contiene informazioni su hello URI dello script hello che è stata eseguita sull'host hello. Ad esempio

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* È possibile creare un cluster di azione script ripetutamente con hello stesso nome. In tal caso, è possibile distinguere i log rilevanti di hello in base al nome di cartella Data hello. Ad esempio, la struttura di cartelle hello per un cluster (mycluster) creato in date diverse appare simile toohello seguenti voci di log:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Se si crea un cluster di azione di script con hello stesso nome in hello stesso giorno, è possibile utilizzare file di log desiderati hello tooidentify hello prefisso univoco.

* Se si crea un cluster quasi 12:00 (mezzanotte), è possibile che i file di log hello estendersi attraverso due giorni. In questi casi, vedrai due cartelle data diversi per hello dello stesso cluster.

* Contenitore predefinito di toohello i file di registro caricamento può richiedere too5 minuti, in particolare per i cluster di grandi dimensioni. In tal caso, se si desidera registri hello tooaccess, è necessario non immediatamente eliminare cluster hello se ha esito negativo di un'azione di script.

### <a name="ambari-watchdog"></a>Watchdog Ambari

> [!WARNING]
> Non modificare la password di hello per hello Ambari Watchdog (hdinsightwatchdog) il cluster HDInsight basati su Linux. La modifica della password per questo account hello interruzioni hello possibilità toorun nuove azioni di script nel cluster HDInsight hello.

### <a name="cant-import-name-blobservice"></a>Non è possibile importare il nome BlobService

__Sintomi__: hello script azione non riuscita. Quando si visualizza l'operazione di hello in Ambari, viene visualizzato toohello simile a testo errore seguente:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Causa__: questo errore si verifica se si esegue l'aggiornamento del client di archiviazione di Azure Python hello incluso con i cluster di HDInsight hello. HDInsight prevede l'uso della versione 0.20.0 del client di archiviazione di Azure.

__Risoluzione__: tooresolve questo errore, connettersi manualmente dei nodi del cluster utilizzando tooeach `ssh` e utilizzare hello seguendo versione client corretta archiviazione di comando tooreinstall hello:

```
sudo pip install azure-storage==0.20.0
```

Per informazioni sulla connessione toohello cluster con SSH, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>La cronologia non mostra gli script usati durante la creazione di un cluster

Se il cluster è stato creato prima del 15 marzo 2016, potrebbe non essere visualizzata una voce nella cronologia delle azioni script. Se si ridimensiona cluster hello dopo 15 marzo 2016, hello script utilizzando durante la creazione del cluster vengono visualizzati nella cronologia applicate toonew nodi nel cluster di hello come parte di hello operazione di ridimensionamento.

Sussistono due eccezioni:

* Se il cluster è stato creato prima del 1° settembre 2015. Le azioni script sono state introdotte in questa data. Per i cluster creati prima di tale data non possono quindi essere state usate le azioni script.

* Se è usato più azioni di Script durante la creazione del cluster e hello stesso nome per più script o hello stesso nome, stesso URI, ma parametri diversi per più script. In questi casi, viene visualizzato il seguente errore hello:

    Nessun nuovo script azioni possono essere eseguito su questo cluster a causa di nomi di script tooconflicting negli script esistenti. I nomi di script forniti durante la creazione del cluster devono essere tutti univoci. Gli script esistenti vengono eseguiti durante il ridimensionamento.

## <a name="next-steps"></a>Passaggi successivi

* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Aggiungere ulteriore spazio di archiviazione tooan HDInsight cluster](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasi durante la creazione di un cluster"
