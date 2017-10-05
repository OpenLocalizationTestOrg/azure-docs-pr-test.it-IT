---
title: Automatizzare Azure Application Insights con PowerShell | Microsoft Docs
description: "Automatizzare la creazione di risorse, avvisi e test di disponibilità in PowerShell usando un modello di Azure Resource Manager."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="a9bf5-103">Creazione di risorse Application Insights con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9bf5-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="a9bf5-104">L'articolo descrive come automatizzare la creazione e l'aggiornamento di risorse di [Application Insights](app-insights-overview.md) usando Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="a9bf5-105">Questo procedimento potrebbe, ad esempio, essere utilizzato come parte di un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="a9bf5-106">Insieme alla risorsa di base di Application Insights, è possibile creare [test Web di disponibilità](app-insights-monitor-web-app-availability.md), configurare [avvisi](app-insights-alerts.md), impostare lo [schema dei prezzi](app-insights-pricing.md) e creare altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="a9bf5-107">La chiave per la creazione di queste risorse è rappresentata dai modelli JSON per [Gestione risorse di Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="a9bf5-108">In breve, la procedura consiste in: scaricare le definizioni JSON delle risorse esistenti; impostare i parametri per determinati valori, come ad esempio nomi; ed eseguire il modello ogni volta che si desidera creare una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="a9bf5-109">È possibile raggruppare diverse risorse per crearle tutte in un’unica volta - ad esempio, un monitoraggio app con test di disponibilità, avvisi e risorsa di archiviazione per l'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="a9bf5-110">Esistono alcune sottigliezze di alcuni parametri, che verranno illustrate di seguito.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="a9bf5-111">Installazione singola</span><span class="sxs-lookup"><span data-stu-id="a9bf5-111">One-time setup</span></span>
<span data-ttu-id="a9bf5-112">Se non si è utilizzato prima PowerShell con la sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="a9bf5-113">Installare il modulo Azure Powershell nel computer in cui si desidera eseguire gli script:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="a9bf5-114">Installare [Installazione guidata piattaforma Web Microsoft (v5 o versione successiva)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="a9bf5-115">Usarla per installare Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="a9bf5-116">Creare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9bf5-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="a9bf5-117">Creare un nuovo file con estensione .json - definirlo `template1.json` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="a9bf5-118">Copiare questo contenuto al suo interno:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter the application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter the application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="a9bf5-119">Creare risorse di Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9bf5-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="a9bf5-120">In PowerShell accedere ad Azure:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="a9bf5-121">Eseguire un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="a9bf5-122">`-ResourceGroupName` è il gruppo in cui si vogliono creare le nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="a9bf5-123">`-TemplateFile` deve precedere i parametri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="a9bf5-124">`-appName` è il nome della risorsa da creare.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="a9bf5-125">È possibile aggiungere altri parametri le cui descrizioni sono disponibili nella sezione del modello dedicata ai parametri.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="a9bf5-126">Per impostare la chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="a9bf5-126">To get the instrumentation key</span></span>
<span data-ttu-id="a9bf5-127">Dopo la creazione di una risorsa applicazione, è necessaria la chiave di strumentazione:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="a9bf5-128">Impostare il piano tariffario</span><span class="sxs-lookup"><span data-stu-id="a9bf5-128">Set the price plan</span></span>

<span data-ttu-id="a9bf5-129">È possibile impostare il [piano tariffario](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="a9bf5-130">Per creare una risorsa app con il piano tariffario Enterprise, usando il modello precedente:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="a9bf5-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="a9bf5-131">priceCode</span></span>|<span data-ttu-id="a9bf5-132">piano</span><span class="sxs-lookup"><span data-stu-id="a9bf5-132">plan</span></span>|
|---|---|
|<span data-ttu-id="a9bf5-133">1</span><span class="sxs-lookup"><span data-stu-id="a9bf5-133">1</span></span>|<span data-ttu-id="a9bf5-134">Basic</span><span class="sxs-lookup"><span data-stu-id="a9bf5-134">Basic</span></span>|
|<span data-ttu-id="a9bf5-135">2</span><span class="sxs-lookup"><span data-stu-id="a9bf5-135">2</span></span>|<span data-ttu-id="a9bf5-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="a9bf5-136">Enterprise</span></span>|

* <span data-ttu-id="a9bf5-137">Se si intende usare solo il piano tariffario Basic predefinito, è possibile omettere la risorsa CurrentBillingFeatures dal modello.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="a9bf5-138">Se si vuole modificare il piano tariffario dopo la creazione della risorsa dei componenti, è possibile usare un modello non contenente la risorsa "microsoft.insights/components".</span><span class="sxs-lookup"><span data-stu-id="a9bf5-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="a9bf5-139">Omettere anche il nodo `dependsOn` nella risorsa della fatturazione.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="a9bf5-140">Per verificare il piano tariffario aggiornato, esaminare il pannello "Funzionalità + prezzi" nel browser.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="a9bf5-141">**Aggiornare la visualizzazione nel browser** per assicurarsi che venga visualizzato lo stato più recente.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="a9bf5-142">Aggiungere un avviso per la metrica</span><span class="sxs-lookup"><span data-stu-id="a9bf5-142">Add a metric alert</span></span>

<span data-ttu-id="a9bf5-143">Per configurare un avviso per la metrica contemporaneamente alla risorsa app, unire il codice seguente nel file modello:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after the app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="a9bf5-144">Quando si richiama il modello, se si vuole, è possibile aggiungere questo parametro:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="a9bf5-145">È possibile impostare parametri anche per altri campi.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="a9bf5-146">Per trovare i nomi dei tipi e i dettagli di configurazione di altre regole di avviso, creare una regola manualmente e quindi esaminarla in [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="a9bf5-147">Aggiungere un test di disponibilità</span><span class="sxs-lookup"><span data-stu-id="a9bf5-147">Add an availability test</span></span>

<span data-ttu-id="a9bf5-148">Questo esempio è relativo a un test di ping (per testare una singola pagina).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="a9bf5-149">**Sono due le parti** di un test di disponibilità: il test stesso e l'avviso che notifica gli errori.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="a9bf5-150">Unire il codice seguente nel file modello che crea l'app.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-150">Merge the following code into the template file that creates the app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="a9bf5-151">Per trovare i codici per altre posizioni di test o per automatizzare la creazione di test Web più complessi, creare un esempio manualmente e quindi impostare i parametri per il codice da [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="a9bf5-152">Aggiungere altre risorse</span><span class="sxs-lookup"><span data-stu-id="a9bf5-152">Add more resources</span></span>

<span data-ttu-id="a9bf5-153">Per automatizzare la creazione di altre risorse di qualsiasi tipo, creare un esempio manualmente e quindi copiare il codice e impostarne i parametri da [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="a9bf5-154">Aprire [Gestione risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="a9bf5-155">Scorrere verso il basso `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components` fino alla risorsa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Navigare in Esplora risorse di Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="a9bf5-157">*Componenti* sono le risorse base di Application Insights per la visualizzazione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="a9bf5-158">Sono disponibili risorse separate per le regole di avviso associate e i test web di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="a9bf5-159">Copiare i JSON del componente nella posizione appropriata in `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="a9bf5-160">Eliminare queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="a9bf5-161">Aprire le sezioni webtests e alertrules e copiare i JSON per i singoli elementi nel modello.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="a9bf5-162">(Non copiare dai nodi webtests e alertrules: passare agli elementi sotto ad essi.)</span><span class="sxs-lookup"><span data-stu-id="a9bf5-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="a9bf5-163">Ciascun test web dispone di una regola di avviso associata, perciò è necessario copiarli entrambi.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="a9bf5-164">È possibile includere anche avvisi nelle metriche.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="a9bf5-165">[Nomi delle metriche](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="a9bf5-166">Inserire questa riga in ciascuna risorsa:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="a9bf5-167">Impostazione dei parametri per il modello</span><span class="sxs-lookup"><span data-stu-id="a9bf5-167">Parameterize the template</span></span>
<span data-ttu-id="a9bf5-168">È necessario sostituire i nomi specifici con i parametri.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="a9bf5-169">Per [impostare i parametri di un modello](../azure-resource-manager/resource-group-authoring-templates.md), si scrivono espressioni mediante un [set di funzioni di supporto](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="a9bf5-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="a9bf5-170">È Impossibile impostare i parametri per una sola parte di una stringa, quindi utilizzare `concat()` per compilare stringhe.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="a9bf5-171">Di seguito sono riportati esempi delle sostituzioni che si possono apportare.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="a9bf5-172">Sono presenti più occorrenze di ogni sostituzione.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="a9bf5-173">Potrebbero esserne necessarie altre nel modello.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-173">You might need others in your template.</span></span> <span data-ttu-id="a9bf5-174">Questi esempi utilizzano i parametri e le variabili definite nella parte superiore del modello.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="a9bf5-175">find</span><span class="sxs-lookup"><span data-stu-id="a9bf5-175">find</span></span> | <span data-ttu-id="a9bf5-176">sostituire con</span><span class="sxs-lookup"><span data-stu-id="a9bf5-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="a9bf5-177">`"myappname"` (minuscolo)</span><span class="sxs-lookup"><span data-stu-id="a9bf5-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="a9bf5-178">Eliminare GUID e ID.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="a9bf5-179">Impostazione di dipendenze tra le risorse</span><span class="sxs-lookup"><span data-stu-id="a9bf5-179">Set dependencies between the resources</span></span>
<span data-ttu-id="a9bf5-180">Azure deve configurare le risorse in ordine fisso.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="a9bf5-181">Per assicurarsi che un programma di installazione venga completato prima che inizi il successivo, aggiungere le righe delle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="a9bf5-182">Nella risorsa del test di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="a9bf5-183">Nella risorsa avviso per un test di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="a9bf5-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9bf5-184">Next steps</span></span>
<span data-ttu-id="a9bf5-185">Altri articoli di automazione:</span><span class="sxs-lookup"><span data-stu-id="a9bf5-185">Other automation articles:</span></span>

* <span data-ttu-id="a9bf5-186">[Creare una risorsa di Application Insights](app-insights-powershell-script-create-resource.md) : metodo rapido che esclude l'uso di un modello.</span><span class="sxs-lookup"><span data-stu-id="a9bf5-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="a9bf5-187">Configurare avvisi</span><span class="sxs-lookup"><span data-stu-id="a9bf5-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="a9bf5-188">Creare test Web</span><span class="sxs-lookup"><span data-stu-id="a9bf5-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="a9bf5-189">Inviare i dati del servizio Diagnostica di Azure ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9bf5-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* <span data-ttu-id="a9bf5-190">[Deploy to Azure from GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx) (Distribuire in Azure da GitHub)</span><span class="sxs-lookup"><span data-stu-id="a9bf5-190">[Deploy to Azure from GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)</span></span>
* [<span data-ttu-id="a9bf5-191">Creare annotazioni di rilascio</span><span class="sxs-lookup"><span data-stu-id="a9bf5-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

