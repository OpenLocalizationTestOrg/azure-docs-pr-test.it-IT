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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="06e22-103">Creare il cluster Hadoop usando hello API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="06e22-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="06e22-104">Informazioni su come toocreate un HDInsight cluster utilizzando un modello di gestione risorse di Azure e hello API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="06e22-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="06e22-105">Hello API REST di Azure consente operazioni di gestione tooperform in servizi ospitati nella piattaforma Azure, inclusa la creazione di nuove risorse, ad esempio cluster HDInsight di hello hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06e22-106">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="06e22-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="06e22-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="06e22-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="06e22-108">passaggi di Hello hello di utilizzare questo documento [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilità con hello API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="06e22-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="06e22-109">Creare un modello</span><span class="sxs-lookup"><span data-stu-id="06e22-109">Create a template</span></span>

<span data-ttu-id="06e22-110">I modelli di Azure Resource Manager sono documenti JSON che descrivono un **gruppo di risorse** e tutte le risorse in esso contenute, ad esempio HDInsight. Questo approccio basato su modello consente risorse hello toodefine che è necessario per HDInsight in un modello.</span><span class="sxs-lookup"><span data-stu-id="06e22-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="06e22-111">Hello documento JSON seguente è una fusione tra società di hello i file di modello e i parametri da [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), che consente di creare basati su Linux cluster utilizzando un hello toosecure password account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="06e22-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

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

<span data-ttu-id="06e22-112">Questo esempio viene utilizzato nei passaggi hello in questo documento.</span><span class="sxs-lookup"><span data-stu-id="06e22-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="06e22-113">Sostituire l'esempio hello *valori* in hello **parametri** sezione con i valori hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="06e22-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06e22-114">modello di Hello utilizza numero predefinito di hello di nodi di lavoro (4) per un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06e22-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="06e22-115">Se si prevedono più di 32 nodi di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="06e22-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="06e22-116">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="06e22-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="06e22-117">Accedi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="06e22-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="06e22-118">Seguire i passaggi di hello documentati in [Introduzione a Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e connettersi tooyour sottoscrizione utilizzando hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="06e22-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="06e22-119">Creare un’entità servizio</span><span class="sxs-lookup"><span data-stu-id="06e22-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="06e22-120">Questi passaggi sono una versione ridotta di hello *creare l'entità servizio con password* sezione di hello [toocreate CLI di Azure di utilizzare un'entità servizio tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) documento.</span><span class="sxs-lookup"><span data-stu-id="06e22-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="06e22-121">Questi passaggi necessari per creare un'entità servizio che viene utilizzato tooauthenticate toohello API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="06e22-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="06e22-122">Dalla riga di comando, utilizzare hello seguente toolist comando le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="06e22-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="06e22-123">Nell'elenco hello selezionare sottoscrizione hello che si desidera toouse e prendere nota di hello **Subscription_ID** e __Tenant_ID__ colonne.</span><span class="sxs-lookup"><span data-stu-id="06e22-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="06e22-124">Salvare questi valori.</span><span class="sxs-lookup"><span data-stu-id="06e22-124">Save these values.</span></span>

2. <span data-ttu-id="06e22-125">Utilizzare hello successivo comando toocreate un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06e22-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="06e22-126">Sostituire i valori hello per hello `--display-name`, `--homepage`, e `--identifier-uris` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="06e22-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="06e22-127">Specificare una password per la nuova voce di Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="06e22-128">Hello `--home-page` e `--identifier-uris` i valori non devono tooreference una pagina web effettivo ospitato in hello internet.</span><span class="sxs-lookup"><span data-stu-id="06e22-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="06e22-129">Devono essere URI univoci.</span><span class="sxs-lookup"><span data-stu-id="06e22-129">They must be unique URIs.</span></span>

   <span data-ttu-id="06e22-130">valore restituito da questo comando Hello è hello __ID App__ per la nuova applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="06e22-131">Salvare il valore.</span><span class="sxs-lookup"><span data-stu-id="06e22-131">Save this value.</span></span>

3. <span data-ttu-id="06e22-132">Comando che segue hello utilizzare toocreate un'entità servizio tramite hello **ID App**.</span><span class="sxs-lookup"><span data-stu-id="06e22-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="06e22-133">valore restituito da questo comando Hello è hello __ID oggetto__.</span><span class="sxs-lookup"><span data-stu-id="06e22-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="06e22-134">Salvare il valore.</span><span class="sxs-lookup"><span data-stu-id="06e22-134">Save this value.</span></span>

4. <span data-ttu-id="06e22-135">Assegnare hello **proprietario** utilizzando hello dell'entità di servizio di ruolo toohello **ID oggetto** valore.</span><span class="sxs-lookup"><span data-stu-id="06e22-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="06e22-136">Hello utilizzare **ID sottoscrizione** ottenuti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06e22-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="06e22-137">Ottenere un token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="06e22-137">Get an authentication token</span></span>

<span data-ttu-id="06e22-138">Utilizzare hello comando tooretrieve un token di autenticazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e22-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="06e22-139">Impostare `$TENANTID`, `$APPID`, e `$PASSWORD` toohello valori ottenuti o utilizzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06e22-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="06e22-140">Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="06e22-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="06e22-141">il documento JSON restituito da questa richiesta Hello contiene un elemento denominato **access_token**.</span><span class="sxs-lookup"><span data-stu-id="06e22-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="06e22-142">valore di Hello **access_token** è usato tooauthentication richieste toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="06e22-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="06e22-143">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="06e22-143">Create a resource group</span></span>

<span data-ttu-id="06e22-144">Utilizzare hello seguente toocreate un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="06e22-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="06e22-145">Impostare `$SUBSCRIPTIONID` ID sottoscrizione toohello ricevuti durante la creazione di un'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="06e22-146">Impostare `$ACCESSTOKEN` token di accesso toohello ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="06e22-147">Sostituire `DATACENTERLOCATION` con data center di hello desiderato, gruppo di risorse toocreate hello e risorse, in.</span><span class="sxs-lookup"><span data-stu-id="06e22-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="06e22-148">Ad esempio "Stati Uniti centrali del sud".</span><span class="sxs-lookup"><span data-stu-id="06e22-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="06e22-149">Impostare `$RESOURCEGROUPNAME` toohello nome toouse per questo gruppo:</span><span class="sxs-lookup"><span data-stu-id="06e22-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="06e22-150">Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON contenente le informazioni sul gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="06e22-151">Hello `"provisioningState"` elemento contiene un valore di `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="06e22-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="06e22-152">Creare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="06e22-152">Create a deployment</span></span>

<span data-ttu-id="06e22-153">Utilizzare hello dopo il gruppo di risorse toohello comando toodeploy hello modello.</span><span class="sxs-lookup"><span data-stu-id="06e22-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="06e22-154">Impostare `$DEPLOYMENTNAME` toohello nome toouse per questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06e22-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="06e22-155">Se è stato salvato hello modello tooa file, è possibile utilizzare hello comando anziché seguente `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="06e22-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="06e22-156">Se la richiesta ha esito positivo, si riceve una risposta 200 serie e corpo della risposta hello contiene un documento JSON contenente informazioni sull'operazione di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06e22-157">distribuzione di Hello è stata inviata, ma non è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e22-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="06e22-158">Può richiedere alcuni minuti, in genere circa 15, hello toocomplete di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06e22-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="06e22-159">Controllare lo stato di hello di una distribuzione</span><span class="sxs-lookup"><span data-stu-id="06e22-159">Check hello status of a deployment</span></span>

<span data-ttu-id="06e22-160">stato di hello toocheck hello della distribuzione di, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="06e22-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="06e22-161">Questo comando restituisce un documento JSON contenente informazioni sull'operazione di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="06e22-162">Hello `"provisioningState"` contiene un elemento dello stato di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="06e22-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="06e22-163">Se questo elemento contiene un valore di `"Succeeded"`, quindi distribuzione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e22-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="06e22-164">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="06e22-164">Troubleshoot</span></span>

<span data-ttu-id="06e22-165">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="06e22-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="06e22-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06e22-166">Next steps</span></span>

<span data-ttu-id="06e22-167">Ora che è stato creato correttamente un cluster HDInsight, utilizzare hello seguente come toolearn toowork con il cluster.</span><span class="sxs-lookup"><span data-stu-id="06e22-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="06e22-168">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="06e22-168">Hadoop clusters</span></span>

* [<span data-ttu-id="06e22-169">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="06e22-170">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="06e22-171">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="06e22-172">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="06e22-172">HBase clusters</span></span>

* [<span data-ttu-id="06e22-173">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="06e22-174">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="06e22-175">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="06e22-175">Storm clusters</span></span>

* [<span data-ttu-id="06e22-176">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="06e22-177">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="06e22-178">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="06e22-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
