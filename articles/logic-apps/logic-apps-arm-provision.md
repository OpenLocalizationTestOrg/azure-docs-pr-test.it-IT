---
title: Creare un'app per la logica usando un modello di Azure | Microsoft Docs
description: Usare un modello di Azure Resource Manager per distribuire un'app per la logica per la definizione dei flussi di lavoro.
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
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="b1961-103">Creare un'app per la logica usando un modello</span><span class="sxs-lookup"><span data-stu-id="b1961-103">Create a Logic App using a template</span></span>
<span data-ttu-id="b1961-104">I modelli rappresentano un modo rapido per usare diversi connettori nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b1961-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="b1961-105">Le app per la logica comprendono i modelli di Azure Resource Manager utili per creare un'app per la logica che può essere utilizzata per definire i flussi di lavoro aziendali.</span><span class="sxs-lookup"><span data-stu-id="b1961-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="b1961-106">Questo consente di definire le risorse da distribuire e le modalità di definizione dei parametri specificati durante l'esecuzione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b1961-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="b1961-107">È possibile usare questo modello per il proprio scenario aziendale o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="b1961-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="b1961-108">Per informazioni dettagliate sulle proprietà delle app per la logica, vedere [API di gestione del flusso di lavoro delle app per la logica](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1961-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="b1961-109">Per esempi della definizione stessa, vedere [Creare definizioni dell'app per la logica](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="b1961-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="b1961-110">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b1961-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b1961-111">Per il modello completo, vedere [Modello di app per la logica](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b1961-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="b1961-112">Cosa viene distribuito</span><span class="sxs-lookup"><span data-stu-id="b1961-112">What you deploy</span></span>
<span data-ttu-id="b1961-113">Con questo modello si distribuisce un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b1961-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="b1961-114">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="b1961-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="b1961-115">[![Distribuzione in Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b1961-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="b1961-116">Parametri</span><span class="sxs-lookup"><span data-stu-id="b1961-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="b1961-117">testUri</span><span class="sxs-lookup"><span data-stu-id="b1961-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="b1961-118">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="b1961-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="b1961-119">App per la logica</span><span class="sxs-lookup"><span data-stu-id="b1961-119">Logic app</span></span>
<span data-ttu-id="b1961-120">Crea l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b1961-120">Creates the logic app.</span></span>

<span data-ttu-id="b1961-121">Il modello usa un valore di parametro per il nome dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b1961-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="b1961-122">Imposta la località dell'app per la logica sulla stessa località del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b1961-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="b1961-123">Questa particolare definizione viene eseguita una volta ogni ora e consente di eseguire il ping del percorso specificato nel parametro **testUri** .</span><span class="sxs-lookup"><span data-stu-id="b1961-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

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


## <a name="commands-to-run-deployment"></a><span data-ttu-id="b1961-124">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b1961-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="b1961-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1961-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="b1961-126">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b1961-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



