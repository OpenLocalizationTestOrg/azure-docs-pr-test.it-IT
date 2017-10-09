---
title: i cluster Hadoop aaaCreate utilizzando l'API REST di Azure - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocreate inviando toohello di modelli di gestione risorse di Azure API REST di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Creare il cluster Hadoop usando hello API REST di Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Informazioni su come toocreate un HDInsight cluster utilizzando un modello di gestione risorse di Azure e hello API REST di Azure.

Hello API REST di Azure consente operazioni di gestione tooperform in servizi ospitati nella piattaforma Azure, inclusa la creazione di nuove risorse, ad esempio cluster HDInsight di hello hello.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!NOTE]
> passaggi di Hello hello di utilizzare questo documento [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilità con hello API REST di Azure.

## <a name="create-a-template"></a>Creare un modello

I modelli di Azure Resource Manager sono documenti JSON che descrivono un **gruppo di risorse** e tutte le risorse in esso contenute, ad esempio HDInsight. Questo approccio basato su modello consente risorse hello toodefine che è necessario per HDInsight in un modello.

Hello documento JSON seguente è una fusione tra società di hello i file di modello e i parametri da [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), che consente di creare basati su Linux cluster utilizzando un hello toosecure password account utente SSH.

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
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
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
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
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

Questo esempio viene utilizzato nei passaggi hello in questo documento. Sostituire l'esempio hello *valori* in hello **parametri** sezione con i valori hello per il cluster.

> [!IMPORTANT]
> modello di Hello utilizza numero predefinito di hello di nodi di lavoro (4) per un cluster HDInsight. Se si prevedono più di 32 nodi di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.
>
> Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Accedi tooyour sottoscrizione di Azure

Seguire i passaggi di hello documentati in [Introduzione a Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e connettersi tooyour sottoscrizione utilizzando hello `az login` comando.

## <a name="create-a-service-principal"></a>Creare un’entità servizio

> [!NOTE]
> Questi passaggi sono una versione ridotta di hello *creare l'entità servizio con password* sezione di hello [toocreate CLI di Azure di utilizzare un'entità servizio tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento. Questi passaggi necessari per creare un'entità servizio che viene utilizzato tooauthenticate toohello API REST di Azure.

1. Dalla riga di comando, utilizzare hello seguente toolist comando le sottoscrizioni di Azure.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Nell'elenco hello selezionare sottoscrizione hello che si desidera toouse e prendere nota di hello **Subscription_ID** e __Tenant_ID__ colonne. Salvare questi valori.

2. Utilizzare hello successivo comando toocreate un'applicazione in Azure Active Directory.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Sostituire i valori hello per hello `--display-name`, `--homepage`, e `--identifier-uris` con valori personalizzati. Specificare una password per la nuova voce di Active Directory hello.

   > [!NOTE]
   > Hello `--home-page` e `--identifier-uris` i valori non devono tooreference una pagina web effettivo ospitato in hello internet. Devono essere URI univoci.

   valore restituito da questo comando Hello è hello __ID App__ per la nuova applicazione hello. Salvare il valore.

3. Comando che segue hello utilizzare toocreate un'entità servizio tramite hello **ID App**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     valore restituito da questo comando Hello è hello __ID oggetto__. Salvare il valore.

4. Assegnare hello **proprietario** utilizzando hello dell'entità di servizio di ruolo toohello **ID oggetto** valore. Hello utilizzare **ID sottoscrizione** ottenuti in precedenza.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Ottenere un token di autenticazione

Utilizzare hello comando tooretrieve un token di autenticazione seguenti:

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Impostare `$TENANTID`, `$APPID`, e `$PASSWORD` toohello valori ottenuti o utilizzata in precedenza.

Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON.

il documento JSON restituito da questa richiesta Hello contiene un elemento denominato **access_token**. valore di Hello **access_token** è usato tooauthentication richieste toohello API REST.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Utilizzare hello seguente toocreate un gruppo di risorse.

* Impostare `$SUBSCRIPTIONID` ID sottoscrizione toohello ricevuti durante la creazione di un'entità servizio hello.
* Impostare `$ACCESSTOKEN` token di accesso toohello ottenuto nel passaggio precedente hello.
* Sostituire `DATACENTERLOCATION` con data center di hello desiderato, gruppo di risorse toocreate hello e risorse, in. Ad esempio "Stati Uniti centrali del sud".
* Impostare `$RESOURCEGROUPNAME` toohello nome toouse per questo gruppo:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON contenente le informazioni sul gruppo hello. Hello `"provisioningState"` elemento contiene un valore di `"Succeeded"`.

## <a name="create-a-deployment"></a>Creare una distribuzione

Utilizzare hello dopo il gruppo di risorse toohello comando toodeploy hello modello.

* Impostare `$DEPLOYMENTNAME` toohello nome toouse per questa distribuzione.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Se è stato salvato hello modello tooa file, è possibile utilizzare hello comando anziché seguente `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON contenente informazioni sull'operazione di distribuzione hello.

> [!IMPORTANT]
> distribuzione di Hello è stata inviata, ma non è stata completata. Può richiedere alcuni minuti, in genere circa 15, hello toocomplete di distribuzione.

## <a name="check-hello-status-of-a-deployment"></a>Controllare lo stato di hello di una distribuzione

stato di hello toocheck hello della distribuzione di, utilizzare hello comando seguente:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

Questo comando restituisce un documento JSON contenente informazioni sull'operazione di distribuzione hello. Hello `"provisioningState"` contiene un elemento dello stato di hello della distribuzione hello. Se questo elemento contiene un valore di `"Succeeded"`, quindi distribuzione hello è stata completata.

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato creato correttamente un cluster HDInsight, utilizzare hello seguente come toolearn toowork con il cluster.

### <a name="hadoop-clusters"></a>Cluster Hadoop

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Cluster HBase

* [Introduzione a HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Sviluppare applicazioni Java per HBase in HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Cluster Storm

* [Sviluppare topologie Java per Storm in HDInsight](hdinsight-storm-develop-java-topology.md)
* [Usare i componenti di Python in Storm in HDInsight](hdinsight-storm-develop-python-topology.md)
* [Distribuire e monitorare le topologie con Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
