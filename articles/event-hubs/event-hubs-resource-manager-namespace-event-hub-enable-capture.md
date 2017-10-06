---
title: un spazio dei nomi di hub eventi di Azure e abilitare l'acquisizione con un modello di aaaCreate | Documenti Microsoft
description: Creare uno spazio dei nomi di Hub eventi di Azure con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="98219-103">Creare uno spazio dei nomi di Hub eventi con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98219-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="98219-104">Questo articolo illustra come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi di hub eventi, a seconda dell'istanza dell'hub un evento e hello consente [la funzionalità di acquisizione](event-hubs-capture-overview.md) nell'hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="98219-104">This article shows how toouse an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables hello [Capture feature](event-hubs-capture-overview.md) on hello event hub.</span></span> <span data-ttu-id="98219-105">Hello articolo viene descritto come toodefine vengono distribuite le risorse e come parametri toodefine specificata se la distribuzione di hello viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="98219-105">hello article describes how toodefine which resources are deployed, and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="98219-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="98219-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="98219-107">In questo articolo inoltre viene illustrata la modalità in base che gli eventi vengono acquisiti in BLOB di archiviazione Azure o un archivio Azure Data Lake toospecify hello destinazione prescelto.</span><span class="sxs-lookup"><span data-stu-id="98219-107">This article also shows how toospecify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on hello destination you choose.</span></span>

<span data-ttu-id="98219-108">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="98219-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="98219-109">Per altre informazioni su procedure e modelli relativi alle convenzioni di denominazione, vedere l'articolo relativo alle [convenzioni di denominazione delle risorse Azure][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="98219-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="98219-110">Per i modelli di hello completo, fare clic su hello seguenti collegamenti di GitHub:</span><span class="sxs-lookup"><span data-stu-id="98219-110">For hello complete templates, click hello following GitHub links:</span></span>

- <span data-ttu-id="98219-111">[Hub e Abilita acquisizione tooStorage modello di evento][Event Hub and enable Capture tooStorage template]</span><span class="sxs-lookup"><span data-stu-id="98219-111">[Event hub and enable Capture tooStorage template][Event Hub and enable Capture tooStorage template]</span></span> 
- <span data-ttu-id="98219-112">[Hub e Abilita acquisizione tooAzure archivio Data Lake modello di evento][Event Hub and enable Capture tooAzure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="98219-112">[Event hub and enable Capture tooAzure Data Lake Store template][Event Hub and enable Capture tooAzure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="98219-113">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per gli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="98219-113">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="98219-114">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="98219-114">What will you deploy?</span></span>

<span data-ttu-id="98219-115">Questo modello consente di distribuire uno spazio dei nomi di Hub eventi con un hub eventi nonché di abilitare la [funzionalità di acquisizione di Hub eventi](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98219-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="98219-116">[Hub eventi](event-hubs-what-is-event-hubs.md) è un evento di elaborazione del servizio utilizzato tooprovide eventi e dati di telemetria in ingresso tooAzure su larga scala, con bassa latenza e affidabilità elevata.</span><span class="sxs-lookup"><span data-stu-id="98219-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="98219-117">Evento hub acquisire Abilita si tooautomatically recapitare hello flusso di dati nell'archiviazione Blob di hub eventi tooAzure o archivio Azure Data Lake, all'interno di un periodo di tempo specificato o un intervallo di dimensioni di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="98219-117">Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooAzure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="98219-118">Fare clic sul seguente pulsante tooenable acquisire gli hub di eventi nell'archiviazione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="98219-118">Click hello following button tooenable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="98219-119">[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="98219-119">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="98219-120">Fare clic sul seguente pulsante tooenable acquisire gli hub di eventi in un archivio Azure Data Lake hello:</span><span class="sxs-lookup"><span data-stu-id="98219-120">Click hello following button tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="98219-121">[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="98219-121">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="98219-122">parameters</span><span class="sxs-lookup"><span data-stu-id="98219-122">Parameters</span></span>

<span data-ttu-id="98219-123">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="98219-124">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="98219-124">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="98219-125">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-125">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="98219-126">Non definire parametri per i valori che restano sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="98219-126">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="98219-127">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="98219-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="98219-128">modello di Hello definisce hello seguenti parametri.</span><span class="sxs-lookup"><span data-stu-id="98219-128">hello template defines hello following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="98219-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="98219-129">eventHubNamespaceName</span></span>

<span data-ttu-id="98219-130">nome Hello di hello [dello spazio dei nomi di hub eventi](event-hubs-create.md) toocreate.</span><span class="sxs-lookup"><span data-stu-id="98219-130">hello name of hello [Event Hubs namespace](event-hubs-create.md) toocreate.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="98219-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="98219-131">eventHubName</span></span>

<span data-ttu-id="98219-132">nome Hello dell'hub di eventi hello creato in hello [dello spazio dei nomi di hub eventi](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="98219-132">hello name of hello event hub created in hello [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="98219-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="98219-133">messageRetentionInDays</span></span>

<span data-ttu-id="98219-134">numero di Hello di messaggi hello tooretain di giorni in hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="98219-134">hello number of days tooretain hello messages in hello event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="98219-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="98219-135">partitionCount</span></span>

<span data-ttu-id="98219-136">numero di Hello di toocreate partizioni nell'hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="98219-136">hello number of partitions toocreate in hello event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="98219-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="98219-137">captureEnabled</span></span>

<span data-ttu-id="98219-138">Abilitare l'acquisizione in hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="98219-138">Enable Capture on hello event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="98219-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="98219-139">captureEncodingFormat</span></span>

<span data-ttu-id="98219-140">formato di codifica Hello è specificare i dati dell'evento tooserialize hello.</span><span class="sxs-lookup"><span data-stu-id="98219-140">hello encoding format you specify tooserialize hello event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="98219-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="98219-141">captureTime</span></span>

<span data-ttu-id="98219-142">intervallo di tempo Hello in cui acquisire gli hub eventi viene avviata l'acquisizione dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-142">hello time interval in which Event Hubs Capture starts capturing hello data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="98219-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="98219-143">captureSize</span></span>
<span data-ttu-id="98219-144">intervallo di dimensioni Hello in cui inizia l'acquisizione dei dati hello acquisizione.</span><span class="sxs-lookup"><span data-stu-id="98219-144">hello size interval at which Capture starts capturing hello data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="98219-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="98219-145">captureNameFormat</span></span>

<span data-ttu-id="98219-146">formato del nome Hello utilizzato dai file di acquisizione di hub eventi toowrite hello Avro.</span><span class="sxs-lookup"><span data-stu-id="98219-146">hello name format used by Event Hubs Capture toowrite hello Avro files.</span></span> <span data-ttu-id="98219-147">Si noti che il formato del nome file di acquisizione deve contenere i campi `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`.</span><span class="sxs-lookup"><span data-stu-id="98219-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="98219-148">Questi campi possono essere disposti in qualsiasi ordine, con o senza delimitatori.</span><span class="sxs-lookup"><span data-stu-id="98219-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="98219-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="98219-149">apiVersion</span></span>

<span data-ttu-id="98219-150">versione di Hello API del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-150">hello API version of hello template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

<span data-ttu-id="98219-151">Utilizzare i seguenti parametri se si sceglie di archiviazione di Azure come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-151">Use hello following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="98219-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="98219-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="98219-153">Acquisizione richiede un tooenable di ID risorsa di account di archiviazione di Azure acquisizione tooyour desiderato di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="98219-153">Capture requires an Azure Storage account resource ID tooenable capturing tooyour desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="98219-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="98219-154">blobContainerName</span></span>

<span data-ttu-id="98219-155">Hello contenitore blob in cui toocapture i dati dell'evento.</span><span class="sxs-lookup"><span data-stu-id="98219-155">hello blob container in which toocapture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

<span data-ttu-id="98219-156">Utilizzare i seguenti parametri se si sceglie archivio Azure Data Lake come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="98219-156">Use hello following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="98219-157">È necessario impostare le autorizzazioni al percorso di archivio Data Lake, in cui si desidera evento hello tooCapture.</span><span class="sxs-lookup"><span data-stu-id="98219-157">You must set permissions on your Data Lake Store path, in which you want tooCapture hello event.</span></span> <span data-ttu-id="98219-158">tooset autorizzazioni, vedere [questo articolo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="98219-158">tooset permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="98219-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="98219-159">subscriptionId</span></span>

<span data-ttu-id="98219-160">ID di sottoscrizione per lo spazio dei nomi di hub eventi hello e archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="98219-160">Subscription ID for hello Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="98219-161">Entrambe queste risorse devono essere gestiti tramite hello stesso ID di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="98219-161">Both these resources must be under hello same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="98219-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="98219-162">dataLakeAccountName</span></span>

<span data-ttu-id="98219-163">nome di archivio Azure Data Lake Hello per hello eventi acquisiti.</span><span class="sxs-lookup"><span data-stu-id="98219-163">hello Azure Data Lake Store name for hello captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="98219-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="98219-164">dataLakeFolderPath</span></span>

<span data-ttu-id="98219-165">percorso di cartella di destinazione di Hello per hello eventi acquisiti.</span><span class="sxs-lookup"><span data-stu-id="98219-165">hello destination folder path for hello captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a><span data-ttu-id="98219-166">Toodeploy risorse di archiviazione di Azure come eventi toocaptured di destinazione</span><span class="sxs-lookup"><span data-stu-id="98219-166">Resources toodeploy for Azure Storage as destination toocaptured events</span></span>

<span data-ttu-id="98219-167">Crea uno spazio dei nomi di tipo **EventHubs**, con l'hub di un evento e consente di acquisire tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="98219-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="98219-168">Risorse toodeploy per archivio Azure Data Lake come destinazione</span><span class="sxs-lookup"><span data-stu-id="98219-168">Resources toodeploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="98219-169">Crea uno spazio dei nomi di tipo **EventHubs**, con l'hub di un evento e consente di archivio Data Lake di acquisizione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="98219-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture tooAzure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="98219-170">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="98219-170">Commands toorun deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="98219-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98219-171">PowerShell</span></span>

<span data-ttu-id="98219-172">Distribuire il tooenable modello acquisire gli hub di eventi nell'archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="98219-172">Deploy your template tooenable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="98219-173">Distribuire il tooenable modello acquisire gli hub di eventi in un archivio Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="98219-173">Deploy your template tooenable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="98219-174">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="98219-174">Azure CLI</span></span>

<span data-ttu-id="98219-175">Scelta di un archivio BLOB di Azure come destinazione:</span><span class="sxs-lookup"><span data-stu-id="98219-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="98219-176">Scelta di Azure Data Lake Store come destinazione:</span><span class="sxs-lookup"><span data-stu-id="98219-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="98219-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98219-177">Next steps</span></span>

<span data-ttu-id="98219-178">È inoltre possibile configurare acquisire gli hub di eventi tramite hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98219-178">You can also configure Event Hubs Capture via hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="98219-179">Per ulteriori informazioni, vedere [abilitare acquisire gli hub eventi utilizzando hello Azure portal](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="98219-179">For more information, see [Enable Event Hubs Capture using hello Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="98219-180">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="98219-180">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="98219-181">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="98219-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="98219-182">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="98219-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="98219-183">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="98219-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
