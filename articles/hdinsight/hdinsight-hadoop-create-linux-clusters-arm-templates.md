---
title: aaaCreate Hadoop cluster utilizzando modelli - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come cluster toocreate per HDInsight utilizzando modelli di gestione risorse
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Creare cluster Hadoop in HDInsight mediante modelli di Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

In questo articolo vengono modi toocreate Azure HDInsight cluster con i modelli di gestione risorse di Azure. Per altre informazioni, vedere [Distribuire un'applicazione con il modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md). toolearn su altri strumenti di creazione del cluster e le funzionalità, fare clic su selettore scheda hello in primo piano hello di questa pagina o vedere [metodi di creazione del Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Prerequisiti
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

istruzioni di hello toofollow in questo articolo, è necessario:

* Una [sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell e/o l'interfaccia della riga di comando di Azure.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Modelli di Gestione risorse
Un modello di gestione risorse rende facile toocreate hello seguenti per l'applicazione in un'operazione singola, coordinata:
* Cluster HDInsight e le relative risorse dipendenti (ad esempio account di archiviazione predefinito hello)
* Altre risorse (ad esempio, Database SQL di Azure toouse Apache Sqoop)

Nel modello di hello, definire le risorse hello necessarie per un'applicazione hello. È inoltre possibile specificare i valori tooinput i parametri di distribuzione per diversi ambienti. modello Hello è costituito da JSON ed espressioni si utilizzano valori tooconstruct per la distribuzione.

È possibile trovare modelli di HDInsight di esempio in [Modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Utilizzare multipiattaforma [codice di Visual Studio](https://code.visualstudio.com/#alt-downloads) con hello [estensione Gestione risorse](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o un modello hello toosave editor di testo in un file nella workstation. Viene illustrato come toocall hello modello utilizzando metodi diversi.

Per ulteriori informazioni sui modelli di gestione delle risorse, vedere hello seguenti articoli:

* [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Distribuire un'applicazione con i modelli di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Generare modelli

Utilizzando hello portale di Azure, è possibile configurare tutte le proprietà di hello di un cluster e quindi salvare il modello di hello prima di distribuirlo. È quindi possibile riutilizzare il modello di hello.

**un modello usando il portale di Azure hello toogenerate**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **New** scegliere dal menu a sinistra, hello **Intelligence + analitica**, quindi fare clic su **HDInsight**.
3. Seguono hello istruzioni tooenter proprietà. È possibile utilizzare entrambi hello **creazione rapida** o hello **personalizzato** opzione.
4. In hello **riepilogo** scheda, fare clic su **Scarica modello e i parametri**:

    ![Download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Verrà visualizzato un elenco di file di modello hello, file dei parametri e modello di codice campioni utilizzati toodeploy hello:

    ![Opzioni di download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    Da qui, si può scaricare il modello di hello, salvarlo tooyour libreria di modelli o distribuire il modello di hello.

    Fare clic su un modello nella libreria, tooaccess **più servizi** dal menu a sinistra di hello e quindi fare clic su **modelli** (in hello **altri** categoria).

    > [!Note]
    > file di modello e i parametri di Hello deve essere usato insieme. in caso contrario, è possibile che si ottengano risultati imprevisti. Ad esempio, hello predefinito **clusterKind** valore della proprietà è sempre **hadoop**, nonostante ciò che si specifica prima di scaricare il modello di hello.



## <a name="deploy-with-powershell"></a>Distribuire con PowerShell

La procedura seguente consente di creare un cluster Hadoop in HDInsight.

1. Salvare il file JSON di hello in hello [appendice](#appx-a-arm-template) tooyour workstation. In uno script di PowerShell hello, il nome di file hello è `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Se necessario, impostare hello parametri e variabili.
3. Eseguire il modello di hello usando hello lo script di PowerShell seguente:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    script di PowerShell Hello configura solo il nome di cluster hello. nome account di archiviazione Hello è hardcoded nel modello di hello. Si è password utente della richiesta tooenter hello cluster. (nome utente predefinito hello **admin**.) Si è anche richiesta tooenter password dell'utente SSH hello. (nome utente SSH predefinito di hello **sshuser**.)  

Per altre informazioni, vedere [Distribuire con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Eseguire la distribuzione con l'interfaccia della riga di comando
Hello seguente esempio Usa Azure interfaccia della riga di comando (CLI). Vengono creati un cluster e i relativi account di archiviazione e contenitore dipendenti chiamando un modello di Resource Manager:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

Si è tooenter richiesta:
* nome del cluster Hello.
* password dell'utente cluster Hello. (nome utente predefinito hello **admin**.)
* password dell'utente SSH Hello. (nome utente SSH predefinito di hello **sshuser**.)

Hello seguente di codice sono disponibili parametri inline:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Distribuire con hello API REST
Vedere [Distribuisci con hello API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Distribuire con Visual Studio
 Usare Visual Studio toocreate un progetto di gruppo di risorse e distribuirlo tooAzure tramite interfaccia utente di hello. Selezionare il tipo di hello di tooinclude risorse nel progetto. Tali risorse vengono aggiunti automaticamente il modello di gestione risorse di toohello. progetto di Hello fornisce anche un modello di hello toodeploy script PowerShell.

Per un'introduzione toousing Visual Studio con gruppi di risorse, vedere [creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight. toolearn informazioni, vedere hello seguenti articoli:

* Per un esempio di distribuzione delle risorse tramite una libreria client .NET di hello, vedere [distribuire le risorse tramite librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Per un esempio dettagliato di distribuzione di un'applicazione, vedere [Effettuare il provisioning di microservizi e distribuirli in modo prevedibile in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Per istruzioni sulla distribuzione negli ambienti toodifferent soluzione, vedere [gli ambienti di sviluppo e test in Microsoft Azure](../solution-dev-test-environments.md).
* toolearn sulle sezioni hello del modello di gestione risorse di Azure hello, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).
* Per un elenco di funzioni hello è possibile utilizzare un modello di gestione risorse di Azure, vedere [funzioni di modello](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Appendice: Gestione risorse modello toocreate un cluster Hadoop
Hello seguente modello di gestione risorse di Azure crea un cluster Hadoop basati su Linux con hello dipendenti account di archiviazione Azure.

> [!NOTE]
> L'esempio include informazioni di configurazione per il metastore Hive e il metastore Oozie. Rimuovere la sezione hello o configurare sezione hello prima di usare il modello di hello.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Appendice: Gestione risorse modello toocreate un cluster Spark

In questa sezione fornisce un modello di gestione risorse che è possibile utilizzare un cluster HDInsight Spark toocreate. Questo modello include le configurazioni per `spark-defaults` e `spark-thrift-sparkconf` (per i cluster Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (per i cluster Spark 2). Inoltre, toothis HDInsight calcola e imposta le configurazioni, ad esempio `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` in base alle dimensioni di cluster hello. 

Se si imposta alcun un parametro in una sezione come parte del modello hello, HDInsight non calcolare e impostare hello altri parametri di hello stessa sezione. Ad esempio, parametro `spark.executor.instances` in hello `spark-defaults` configurazione. Se si imposta un altro parametro (ad esempio, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configurazione, HDInsight non calcolare e impostare hello `spark.executor.instances` nonché parametro.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
