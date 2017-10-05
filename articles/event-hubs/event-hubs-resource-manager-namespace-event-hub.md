---
title: Creare un gruppo di consumer e lo spazio dei nomi di Hub eventi di Azure usando un modello | Documentazione Microsoft
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
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="dc6c0-103">Creare uno spazio dei nomi Hub eventi con hub eventi e gruppo di consumer usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc6c0-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="dc6c0-104">Questo articolo illustra come usare un modello di Azure Resource Manager per creare uno spazio dei nomi di tipo Hub eventi con un hub eventi e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="dc6c0-105">L'articolo descrive come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="dc6c0-106">È possibile usare questo modello per la distribuzione o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="dc6c0-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="dc6c0-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="dc6c0-108">Per il modello completo, vedere il [modello di Hub eventi e gruppo di consumer][Event Hub and consumer group template] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="dc6c0-109">Per verificare gli ultimi modelli, vedere la raccolta [Modelli di avvio rapido di Azure][Azure Quickstart Templates] e cercare Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="dc6c0-110">Distribuzione</span><span class="sxs-lookup"><span data-stu-id="dc6c0-110">What will you deploy?</span></span>
<span data-ttu-id="dc6c0-111">Questo modello consente di distribuire uno spazio dei nomi di Hub eventi con un hub eventi e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="dc6c0-112">[Hub eventi](event-hubs-what-is-event-hubs.md) è un servizio di elaborazione di eventi che viene usato per fornire eventi e dati di telemetria in entrata in Azure su larga scala, con bassa latenza ed elevata affidabilità.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="dc6c0-113">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="dc6c0-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="dc6c0-114">[![Distribuzione in Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="dc6c0-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="dc6c0-115">Parametri</span><span class="sxs-lookup"><span data-stu-id="dc6c0-115">Parameters</span></span>
<span data-ttu-id="dc6c0-116">Gestione risorse di Azure permette di definire i parametri per i valori da specificare durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="dc6c0-117">Il modello include una sezione denominata `Parameters` che contiene tutti i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="dc6c0-118">È opportuno definire un parametro per i valori che varieranno, in base al progetto che si sta distribuendo o all'ambiente in cui si esegue la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="dc6c0-119">Non definire i parametri per i valori che rimangono invariati.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="dc6c0-120">Ogni valore di parametro nel modello definisce le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="dc6c0-121">Il modello definisce i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc6c0-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="dc6c0-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="dc6c0-122">eventHubNamespaceName</span></span>
<span data-ttu-id="dc6c0-123">Nome dello spazio dei nomi dell'hub eventi da creare.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="dc6c0-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="dc6c0-124">eventHubName</span></span>
<span data-ttu-id="dc6c0-125">Nome dell'hub eventi creato nello spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="dc6c0-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="dc6c0-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="dc6c0-127">Nome del gruppo di consumer creato per l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="dc6c0-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dc6c0-128">apiVersion</span></span>
<span data-ttu-id="dc6c0-129">Versione API del modello.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="dc6c0-130">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="dc6c0-130">Resources to deploy</span></span>
<span data-ttu-id="dc6c0-131">Crea uno spazio dei nomi di tipo **Hub eventi**con un hub eventi e un gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="dc6c0-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="dc6c0-132">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="dc6c0-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="dc6c0-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc6c0-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="dc6c0-134">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dc6c0-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="dc6c0-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc6c0-135">Next steps</span></span>
<span data-ttu-id="dc6c0-136">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc6c0-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="dc6c0-137">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="dc6c0-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="dc6c0-138">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="dc6c0-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="dc6c0-139">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="dc6c0-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
