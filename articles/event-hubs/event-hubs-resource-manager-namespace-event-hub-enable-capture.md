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
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Creare uno spazio dei nomi di Hub eventi con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager

Questo articolo illustra come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi di hub eventi, a seconda dell'istanza dell'hub un evento e hello consente [la funzionalità di acquisizione](event-hubs-capture-overview.md) nell'hub eventi hello. Hello articolo viene descritto come toodefine vengono distribuite le risorse e come parametri toodefine specificata se la distribuzione di hello viene eseguita. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.

In questo articolo inoltre viene illustrata la modalità in base che gli eventi vengono acquisiti in BLOB di archiviazione Azure o un archivio Azure Data Lake toospecify hello destinazione prescelto.

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].

Per altre informazioni su procedure e modelli relativi alle convenzioni di denominazione, vedere l'articolo relativo alle [convenzioni di denominazione delle risorse Azure][Azure Resources naming conventions].

Per i modelli di hello completo, fare clic su hello seguenti collegamenti di GitHub:

- [Hub e Abilita acquisizione tooStorage modello di evento][Event Hub and enable Capture tooStorage template] 
- [Hub e Abilita acquisizione tooAzure archivio Data Lake modello di evento][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per gli hub eventi.
> 
> 

## <a name="what-will-you-deploy"></a>Distribuzione

Questo modello consente di distribuire uno spazio dei nomi di Hub eventi con un hub eventi nonché di abilitare la [funzionalità di acquisizione di Hub eventi](event-hubs-capture-overview.md).

[Hub eventi](event-hubs-what-is-event-hubs.md) è un evento di elaborazione del servizio utilizzato tooprovide eventi e dati di telemetria in ingresso tooAzure su larga scala, con bassa latenza e affidabilità elevata. Evento hub acquisire Abilita si tooautomatically recapitare hello flusso di dati nell'archiviazione Blob di hub eventi tooAzure o archivio Azure Data Lake, all'interno di un periodo di tempo specificato o un intervallo di dimensioni di propria scelta.

Fare clic sul seguente pulsante tooenable acquisire gli hub di eventi nell'archiviazione di Azure hello:

[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Fare clic sul seguente pulsante tooenable acquisire gli hub di eventi in un archivio Azure Data Lake hello:

[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>parameters

Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello. È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che restano sempre hello stesso. Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.

modello di Hello definisce hello seguenti parametri.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

nome Hello di hello [dello spazio dei nomi di hub eventi](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

nome Hello dell'hub di eventi hello creato in hello [dello spazio dei nomi di hub eventi](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

numero di Hello di messaggi hello tooretain di giorni in hub eventi hello. 

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

### <a name="partitioncount"></a>partitionCount

numero di Hello di toocreate partizioni nell'hub eventi hello.

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

### <a name="captureenabled"></a>captureEnabled

Abilitare l'acquisizione in hub eventi hello.

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
### <a name="captureencodingformat"></a>captureEncodingFormat

formato di codifica Hello è specificare i dati dell'evento tooserialize hello.

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

### <a name="capturetime"></a>captureTime

intervallo di tempo Hello in cui acquisire gli hub eventi viene avviata l'acquisizione dei dati di hello.

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

### <a name="capturesize"></a>captureSize
intervallo di dimensioni Hello in cui inizia l'acquisizione dei dati hello acquisizione.

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

###<a name="capturenameformat"></a>captureNameFormat

formato del nome Hello utilizzato dai file di acquisizione di hub eventi toowrite hello Avro. Si noti che il formato del nome file di acquisizione deve contenere i campi `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` e `{Second}`. Questi campi possono essere disposti in qualsiasi ordine, con o senza delimitatori.
 
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

### <a name="apiversion"></a>apiVersion

versione di Hello API del modello di hello.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Utilizzare i seguenti parametri se si sceglie di archiviazione di Azure come destinazione di hello.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Acquisizione richiede un tooenable di ID risorsa di account di archiviazione di Azure acquisizione tooyour desiderato di account di archiviazione.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

Hello contenitore blob in cui toocapture i dati dell'evento.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Utilizzare i seguenti parametri se si sceglie archivio Azure Data Lake come destinazione di hello. È necessario impostare le autorizzazioni al percorso di archivio Data Lake, in cui si desidera evento hello tooCapture. tooset autorizzazioni, vedere [questo articolo](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

ID di sottoscrizione per lo spazio dei nomi di hub eventi hello e archivio Azure Data Lake. Entrambe queste risorse devono essere gestiti tramite hello stesso ID di sottoscrizione.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

nome di archivio Azure Data Lake Hello per hello eventi acquisiti.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

percorso di cartella di destinazione di Hello per hello eventi acquisiti.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Toodeploy risorse di archiviazione di Azure come eventi toocaptured di destinazione

Crea uno spazio dei nomi di tipo **EventHubs**, con l'hub di un evento e consente di acquisire tooAzure nell'archiviazione Blob.

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Risorse toodeploy per archivio Azure Data Lake come destinazione

Crea uno spazio dei nomi di tipo **EventHubs**, con l'hub di un evento e consente di archivio Data Lake di acquisizione tooAzure.

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

## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Distribuire il tooenable modello acquisire gli hub di eventi nell'archiviazione di Azure:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Distribuire il tooenable modello acquisire gli hub di eventi in un archivio Azure Data Lake:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Scelta di un archivio BLOB di Azure come destinazione:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Scelta di Azure Data Lake Store come destinazione:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Passaggi successivi

È inoltre possibile configurare acquisire gli hub di eventi tramite hello [portale di Azure](https://portal.azure.com). Per ulteriori informazioni, vedere [abilitare acquisire gli hub eventi utilizzando hello Azure portal](event-hubs-capture-enable-through-portal.md).

Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
