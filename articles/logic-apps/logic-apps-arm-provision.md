---
title: aaaCreate un'app di logica utilizzando un modello in Azure | Documenti Microsoft
description: Utilizzare un toodeploy modello di gestione risorse di Azure un'app per la logica per la definizione di flussi di lavoro.
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="0db90-103">Creare un'app per la logica usando un modello</span><span class="sxs-lookup"><span data-stu-id="0db90-103">Create a Logic App using a template</span></span>
<span data-ttu-id="0db90-104">I modelli offrono toouse un modo rapido connettori diversi all'interno di un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="0db90-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="0db90-105">Logica App include modelli di gestione risorse di Azure per si toocreate un'app di logica che può essere utilizzati toodefine flussi di lavoro aziendali.</span><span class="sxs-lookup"><span data-stu-id="0db90-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="0db90-106">È possibile definire le risorse vengono distribuite e come parametri toodefine quando si distribuisce l'app logica.</span><span class="sxs-lookup"><span data-stu-id="0db90-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="0db90-107">È possibile utilizzare questo modello per i propri scenari di business o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="0db90-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="0db90-108">Per ulteriori informazioni sulle proprietà dell'app hello logica, vedere [API di gestione del flusso di lavoro logica App](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="0db90-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="0db90-109">Per esempi di definizione hello, vedere [definizioni autore logica App](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="0db90-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="0db90-110">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0db90-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0db90-111">Per il modello di hello completo, vedere [modello logica App](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="0db90-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="0db90-112">Cosa viene distribuito</span><span class="sxs-lookup"><span data-stu-id="0db90-112">What you deploy</span></span>
<span data-ttu-id="0db90-113">Con questo modello si distribuisce un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0db90-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="0db90-114">distribuzione di hello toorun automaticamente, selezionare hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="0db90-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="0db90-115">[![Distribuire tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0db90-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="0db90-116">parameters</span><span class="sxs-lookup"><span data-stu-id="0db90-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="0db90-117">testUri</span><span class="sxs-lookup"><span data-stu-id="0db90-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="0db90-118">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="0db90-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="0db90-119">App per la logica</span><span class="sxs-lookup"><span data-stu-id="0db90-119">Logic app</span></span>
<span data-ttu-id="0db90-120">Crea app logica hello.</span><span class="sxs-lookup"><span data-stu-id="0db90-120">Creates hello logic app.</span></span>

<span data-ttu-id="0db90-121">modelli di Hello utilizza un valore di parametro per nome dell'applicazione hello logica.</span><span class="sxs-lookup"><span data-stu-id="0db90-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="0db90-122">Imposta percorso hello di hello logica app toohello stesso percorso del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="0db90-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="0db90-123">Questa definizione particolare viene eseguito una volta all'ora e ping hello posizione specificata in hello **testUri** parametro.</span><span class="sxs-lookup"><span data-stu-id="0db90-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a><span data-ttu-id="0db90-124">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="0db90-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="0db90-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0db90-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="0db90-126">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0db90-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



