---
title: un gruppo di spazio dei nomi e i consumer di hub eventi di Azure utilizzando un modello aaaCreate | Documenti Microsoft
description: Creare uno spazio dei nomi dell'hub eventi con Hub eventi e un gruppo di consumer usando i modelli di Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="2bb01-103">Creare uno spazio dei nomi Hub eventi con hub eventi e gruppo di consumer usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2bb01-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="2bb01-104">In questo articolo viene illustrato come toouse un modello di gestione risorse di Azure che crea uno spazio dei nomi di tipo hub eventi, con l'hub di un evento e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="2bb01-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="2bb01-105">Hello articolo viene illustrato come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="2bb01-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="2bb01-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet i requisiti</span><span class="sxs-lookup"><span data-stu-id="2bb01-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="2bb01-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="2bb01-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="2bb01-108">Per il modello di hello completo, vedere hello [modello gruppo di hub e consumer di eventi] [ Event Hub and consumer group template] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="2bb01-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="2bb01-109">toocheck per i modelli più recenti di hello, visitare hello [modelli di avvio rapido di Azure] [ Azure Quickstart Templates] raccolta e la ricerca per gli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2bb01-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="2bb01-110">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="2bb01-110">What will you deploy?</span></span>
<span data-ttu-id="2bb01-111">Questo modello consente di distribuire uno spazio dei nomi di Hub eventi con un hub eventi e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="2bb01-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="2bb01-112">[Hub eventi](event-hubs-what-is-event-hubs.md) è un evento di elaborazione del servizio utilizzato tooprovide eventi e dati di telemetria in ingresso tooAzure su larga scala, con bassa latenza e affidabilità elevata.</span><span class="sxs-lookup"><span data-stu-id="2bb01-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="2bb01-113">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="2bb01-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="2bb01-114">[![Distribuire tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="2bb01-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="2bb01-115">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb01-115">Parameters</span></span>
<span data-ttu-id="2bb01-116">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="2bb01-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="2bb01-117">modello Hello include una sezione denominata `Parameters` che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="2bb01-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="2bb01-118">È necessario definire un parametro per i valori che possono variare, basato su progetto hello che si distribuisce o su hello ambiente toowhich che si sta distribuendo.</span><span class="sxs-lookup"><span data-stu-id="2bb01-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="2bb01-119">Non definire parametri per i valori che restano sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="2bb01-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="2bb01-120">Ogni valore del parametro nel modello hello definisce le risorse hello distribuite.</span><span class="sxs-lookup"><span data-stu-id="2bb01-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="2bb01-121">modello di Hello definisce hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="2bb01-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="2bb01-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="2bb01-122">eventHubNamespaceName</span></span>
<span data-ttu-id="2bb01-123">nome Hello del toocreate dello spazio dei nomi di hello hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2bb01-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="2bb01-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="2bb01-124">eventHubName</span></span>
<span data-ttu-id="2bb01-125">nome Hello dell'hub di eventi hello creato nello spazio dei nomi di hello hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2bb01-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="2bb01-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="2bb01-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="2bb01-127">nome Hello del gruppo di consumer hello creato per l'hub di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="2bb01-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="2bb01-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2bb01-128">apiVersion</span></span>
<span data-ttu-id="2bb01-129">versione di Hello API del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="2bb01-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="2bb01-130">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="2bb01-130">Resources toodeploy</span></span>
<span data-ttu-id="2bb01-131">Crea uno spazio dei nomi di tipo **Hub eventi**con un hub eventi e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="2bb01-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="2bb01-132">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="2bb01-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="2bb01-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bb01-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="2bb01-134">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2bb01-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="2bb01-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bb01-135">Next steps</span></span>
<span data-ttu-id="2bb01-136">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="2bb01-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="2bb01-137">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2bb01-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2bb01-138">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="2bb01-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="2bb01-139">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2bb01-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
