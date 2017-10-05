---
title: Creare i cluster Hadoop tramite l'interfaccia dell'API REST di Azure | Microsoft Docs
description: Informazioni su come creare cluster HDInsight inviando i modelli di Azure Resource Manager all'API REST di Azure.
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="fa4cf-103">Creare i cluster Hadoop tramite l'API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="fa4cf-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="fa4cf-104">Informazioni su come creare un cluster HDInsight tramite un modello di Azure Resource Manager e l'API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="fa4cf-105">L'API REST di Azure consente di eseguire operazioni di gestione su servizi ospitati nella piattaforma Azure, inclusa la creazione di nuove risorse, ad esempio cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa4cf-106">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fa4cf-107">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fa4cf-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="fa4cf-108">La procedura descritta in questo documento usa l'utilità [curl (https://curl.haxx.se/)](https://curl.haxx.se/) per comunicare con l'API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="fa4cf-109">Creare un modello</span><span class="sxs-lookup"><span data-stu-id="fa4cf-109">Create a template</span></span>

<span data-ttu-id="fa4cf-110">I modelli di Azure Resource Manager sono documenti JSON che descrivono un **gruppo di risorse** e tutte le risorse in esso contenute, ad esempio HDInsight. Questo approccio basato su modelli consente di definire le risorse necessarie per HDInsight in un singolo modello.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="fa4cf-111">Il documento JSON seguente è una fusione dei file di modello e di parametri ricavati da [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), che consente di creare un cluster basato su Linux usando una password per proteggere l'account utente SSH.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="fa4cf-112">Questo esempio viene usato nei passaggi di questo documento.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="fa4cf-113">Sostituire i *valori* di esempio nella sezione **Parametri** con i valori relativi al cluster in uso.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa4cf-114">Il modello usa il numero di nodi di lavoro predefinito (4) per un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="fa4cf-115">Se si prevedono più di 32 nodi di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="fa4cf-116">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fa4cf-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="fa4cf-117">Accedere alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="fa4cf-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="fa4cf-118">Seguire i passaggi illustrati [Introduzione all'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) e connettersi alla sottoscrizione tramite il comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="fa4cf-119">Creare un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="fa4cf-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="fa4cf-120">Questa procedura costituisce una sintesi della sezione *Creare un'entità servizio con password* dell'articolo [Usare l'interfaccia della riga di comando di Azure per creare un'entità servizio per accedere alle risorse](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="fa4cf-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="fa4cf-121">Con questi passaggi viene creata un'entità servizio usata per autenticare l'API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="fa4cf-122">Dalla riga di comando, usare il comando seguente per elencare le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="fa4cf-123">Nell'elenco selezionare la sottoscrizione che si vuole usare e annotare i valori nelle colonne **Subscription_ID** e __Tenant_ID__.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="fa4cf-124">Salvare questi valori.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-124">Save these values.</span></span>

2. <span data-ttu-id="fa4cf-125">Eseguire i comandi seguenti per creare un'applicazione in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="fa4cf-126">Sostituire i valori di `--display-name`, `--homepage` e `--identifier-uris` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="fa4cf-127">Specificare una password per la nuova voce di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa4cf-128">I valori `--home-page` e `--identifier-uris` non devono fare riferimento a una pagina Web reale ospitata in Internet.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="fa4cf-129">Devono essere URI univoci.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-129">They must be unique URIs.</span></span>

   <span data-ttu-id="fa4cf-130">Il valore restituito da questo comando è l'__ID app__ per la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="fa4cf-131">Salvare il valore.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-131">Save this value.</span></span>

3. <span data-ttu-id="fa4cf-132">Eseguire il comando seguente per creare un'entità servizio mediante l'**ID app**.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="fa4cf-133">Il valore restituito da questo comando è l'__ID oggetto__.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="fa4cf-134">Salvare il valore.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-134">Save this value.</span></span>

4. <span data-ttu-id="fa4cf-135">Assegnare il ruolo **Owner** all'entità servizio usando il valore **ID oggetto** precedentemente restituito.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="fa4cf-136">Usare anche l'**ID sottoscrizione** ottenuto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="fa4cf-137">Ottenere un token di autenticazione</span><span class="sxs-lookup"><span data-stu-id="fa4cf-137">Get an authentication token</span></span>

<span data-ttu-id="fa4cf-138">Usare il comando seguente per recuperare un token di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="fa4cf-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="fa4cf-139">Impostare `$TENANTID`, `$APPID` e `$PASSWORD` per i valori ottenuti o usati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="fa4cf-140">Se la richiesta ha esito positivo, si riceve una risposta serie 200 e il corpo della risposta contiene un documento JSON.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="fa4cf-141">Il documento JSON restituito da questa richiesta contiene un elemento denominato **access_token**.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="fa4cf-142">Il valore di **access_token** viene usato per le richieste di autenticazione all'API REST.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fa4cf-143">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="fa4cf-143">Create a resource group</span></span>

<span data-ttu-id="fa4cf-144">Per creare un gruppo di risorse, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="fa4cf-145">Impostare `$SUBSCRIPTIONID` sull'ID sottoscrizione ricevuto durante la creazione dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="fa4cf-146">Impostare `$ACCESSTOKEN` sul token di accesso ricevuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="fa4cf-147">Sostituire `DATACENTERLOCATION` con il data center in cui si vuole creare il gruppo di risorse e le risorse.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="fa4cf-148">Ad esempio "Stati Uniti centrali del sud".</span><span class="sxs-lookup"><span data-stu-id="fa4cf-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="fa4cf-149">Impostare `$RESOURCEGROUPNAME` sul nome che si vuole usare per questo gruppo:</span><span class="sxs-lookup"><span data-stu-id="fa4cf-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="fa4cf-150">Se la richiesta ha esito positivo, si riceve una risposta serie 200 e il corpo della risposta contiene un documento JSON che include le informazioni del gruppo.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="fa4cf-151">L'elemento `"provisioningState"` contiene un valore di `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="fa4cf-152">Creare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="fa4cf-152">Create a deployment</span></span>

<span data-ttu-id="fa4cf-153">Usare il comando seguente per distribuire il modello nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="fa4cf-154">Impostare `$DEPLOYMENTNAME` sul nome che si vuole usare per questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="fa4cf-155">Se il modello è stato salvato in un file, è possibile usare il comando seguente invece di `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="fa4cf-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="fa4cf-156">Se la richiesta ha esito positivo, si riceve una risposta serie 200 e il corpo della risposta contiene un documento JSON che include le informazioni dell'operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa4cf-157">La distribuzione è stata inviata, ma non è stata completata.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="fa4cf-158">Possono essere necessari diversi minuti, in genere circa 15, per completare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="fa4cf-159">Controllare lo stato di una distribuzione</span><span class="sxs-lookup"><span data-stu-id="fa4cf-159">Check the status of a deployment</span></span>

<span data-ttu-id="fa4cf-160">Per verificare lo stato della distribuzione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa4cf-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="fa4cf-161">Questo comando restituisce un documento JSON che contiene informazioni sull'operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="fa4cf-162">L'elemento `"provisioningState"` contiene lo stato della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="fa4cf-163">Se questo elemento contiene un valore di `"Succeeded"`, la distribuzione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="fa4cf-164">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="fa4cf-164">Troubleshoot</span></span>

<span data-ttu-id="fa4cf-165">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="fa4cf-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa4cf-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa4cf-166">Next steps</span></span>

<span data-ttu-id="fa4cf-167">Dopo aver creato un cluster HDInsight, usare le informazioni seguenti per acquisire familiarità con il cluster.</span><span class="sxs-lookup"><span data-stu-id="fa4cf-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="fa4cf-168">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="fa4cf-168">Hadoop clusters</span></span>

* [<span data-ttu-id="fa4cf-169">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fa4cf-170">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="fa4cf-171">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="fa4cf-172">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="fa4cf-172">HBase clusters</span></span>

* [<span data-ttu-id="fa4cf-173">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="fa4cf-174">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="fa4cf-175">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="fa4cf-175">Storm clusters</span></span>

* [<span data-ttu-id="fa4cf-176">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="fa4cf-177">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="fa4cf-178">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="fa4cf-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
