---
title: aaaAutomate Azure Application Insights con PowerShell | Documenti Microsoft
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
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="54ca0-103">Creazione di risorse Application Insights con PowerShell</span><span class="sxs-lookup"><span data-stu-id="54ca0-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="54ca0-104">Questo articolo illustra come tooautomate hello creazione e l'aggiornamento di [Application Insights](app-insights-overview.md) risorse automaticamente, usando Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="54ca0-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="54ca0-105">Questo procedimento potrebbe, ad esempio, essere utilizzato come parte di un processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="54ca0-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="54ca0-106">Insieme a risorsa di Application Insights hello base, è possibile creare [test web disponibilità](app-insights-monitor-web-app-availability.md), impostare i [avvisi](app-insights-alerts.md), hello impostare [prezzi schema](app-insights-pricing.md)e creare altre Azure risorse.</span><span class="sxs-lookup"><span data-stu-id="54ca0-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="54ca0-107">Hello toocreating chiave queste risorse è modelli JSON per [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="54ca0-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="54ca0-108">In breve, la procedura hello è: scaricare le definizioni di JSON hello di risorse esistente. parametrizzare determinati valori, ad esempio nomi; e quindi eseguire il modello di hello ogni volta che si desidera toocreate una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="54ca0-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="54ca0-109">È possibile distribuire contemporaneamente più risorse, toocreate che tutti in uno proseguire, ad esempio, un monitoraggio di app con i test di disponibilità, avvisi e archiviazione per l'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="54ca0-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="54ca0-110">Esistono alcuni toosome sfumature parametrizzazioni hello, che verrà illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="54ca0-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="54ca0-111">Installazione singola</span><span class="sxs-lookup"><span data-stu-id="54ca0-111">One-time setup</span></span>
<span data-ttu-id="54ca0-112">Se non si è mai usato PowerShell con la sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="54ca0-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="54ca0-113">Installare il modulo di Azure Powershell hello computer hello in cui si desidera script hello toorun:</span><span class="sxs-lookup"><span data-stu-id="54ca0-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="54ca0-114">Installare [Installazione guidata piattaforma Web Microsoft (v5 o versione successiva)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="54ca0-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="54ca0-115">Usarlo tooinstall Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="54ca0-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="54ca0-116">Creare un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54ca0-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="54ca0-117">Creare un nuovo file con estensione .json - definirlo `template1.json` in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="54ca0-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="54ca0-118">Copiare questo contenuto al suo interno:</span><span class="sxs-lookup"><span data-stu-id="54ca0-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
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
                    "description": "Enter hello application type."
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
                    "description": "Enter hello application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="54ca0-119">Creare risorse di Application Insights</span><span class="sxs-lookup"><span data-stu-id="54ca0-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="54ca0-120">In PowerShell, eseguire l'accesso tooAzure:</span><span class="sxs-lookup"><span data-stu-id="54ca0-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="54ca0-121">Eseguire un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="54ca0-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="54ca0-122">`-ResourceGroupName`è il gruppo di hello in cui si desidera nuove risorse di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="54ca0-123">`-TemplateFile`deve essere precedente parametri personalizzati hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="54ca0-124">`-appName`nome Hello di hello risorsa toocreate.</span><span class="sxs-lookup"><span data-stu-id="54ca0-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="54ca0-125">È possibile aggiungere altri parametri, le relative descrizioni sono disponibili nella sezione parametri hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="54ca0-126">chiave di strumentazione hello tooget</span><span class="sxs-lookup"><span data-stu-id="54ca0-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="54ca0-127">Dopo la creazione di una risorsa dell'applicazione, è necessario che la chiave di strumentazione hello:</span><span class="sxs-lookup"><span data-stu-id="54ca0-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="54ca0-128">Piano di prezzo hello set</span><span class="sxs-lookup"><span data-stu-id="54ca0-128">Set hello price plan</span></span>

<span data-ttu-id="54ca0-129">È possibile impostare hello [piano prezzo](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="54ca0-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="54ca0-130">toocreate una risorsa app hello Enterprise prezzo piano, utilizzando hello modello precedente:</span><span class="sxs-lookup"><span data-stu-id="54ca0-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="54ca0-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="54ca0-131">priceCode</span></span>|<span data-ttu-id="54ca0-132">piano</span><span class="sxs-lookup"><span data-stu-id="54ca0-132">plan</span></span>|
|---|---|
|<span data-ttu-id="54ca0-133">1</span><span class="sxs-lookup"><span data-stu-id="54ca0-133">1</span></span>|<span data-ttu-id="54ca0-134">Basic</span><span class="sxs-lookup"><span data-stu-id="54ca0-134">Basic</span></span>|
|<span data-ttu-id="54ca0-135">2</span><span class="sxs-lookup"><span data-stu-id="54ca0-135">2</span></span>|<span data-ttu-id="54ca0-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="54ca0-136">Enterprise</span></span>|

* <span data-ttu-id="54ca0-137">Se si desidera solo il piano toouse hello predefinito prezzo di base, è possibile omettere risorsa CurrentBillingFeatures hello dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="54ca0-138">Se si vuole piano di prezzo hello toochange dopo risorse componente hello sono stata creata, è possibile utilizzare un modello che include risorse "microsoft.insights/components" hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="54ca0-139">Inoltre, omettere hello `dependsOn` nodo da hello fatturazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="54ca0-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="54ca0-140">tooverify hello piano prezzo aggiornato, esaminare il pannello hello "Funzionalità + prezzi" nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="54ca0-141">**Aggiorna visualizzazione esplorazione hello** toomake che sia possibile visualizzare lo stato più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="54ca0-142">Aggiungere un avviso per la metrica</span><span class="sxs-lookup"><span data-stu-id="54ca0-142">Add a metric alert</span></span>

<span data-ttu-id="54ca0-143">tooset di un avviso di metriche in hello stesso tempo come risorsa app, codice di tipo merge simile al seguente nel file di modello hello:</span><span class="sxs-lookup"><span data-stu-id="54ca0-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

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
      // Ensure this resource is created after hello app resource:
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

<span data-ttu-id="54ca0-144">Quando si richiama il modello di hello, è possibile aggiungere facoltativamente questo parametro:</span><span class="sxs-lookup"><span data-stu-id="54ca0-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="54ca0-145">È possibile impostare parametri anche per altri campi.</span><span class="sxs-lookup"><span data-stu-id="54ca0-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="54ca0-146">toofind nomi di tipo hello e i dettagli di configurazione di altre regole di avviso, creare manualmente una regola e quindi controllare in [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="54ca0-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="54ca0-147">Aggiungere un test di disponibilità</span><span class="sxs-lookup"><span data-stu-id="54ca0-147">Add an availability test</span></span>

<span data-ttu-id="54ca0-148">Questo esempio è per un test di ping (tootest una singola pagina).</span><span class="sxs-lookup"><span data-stu-id="54ca0-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="54ca0-149">**Esistono due parti** in un test di disponibilità: test di hello e avviso hello di notifica di errori.</span><span class="sxs-lookup"><span data-stu-id="54ca0-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="54ca0-150">Merge hello seguente codice nel file di modello hello che crea l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-150">Merge hello following code into hello template file that creates hello app.</span></span>

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
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
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

<span data-ttu-id="54ca0-151">codici di hello toodiscover per altre posizioni di test o la creazione di hello tooautomate di test web più complesse, creare manualmente un esempio e quindi parametrizzare codice hello da [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="54ca0-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="54ca0-152">Aggiungere altre risorse</span><span class="sxs-lookup"><span data-stu-id="54ca0-152">Add more resources</span></span>

<span data-ttu-id="54ca0-153">creazione di hello tooautomate di qualsiasi altra risorsa di qualsiasi tipo, creare un esempio in modo manuale e quindi copiare e parametrizzare il codice da [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="54ca0-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="54ca0-154">Aprire [Gestione risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="54ca0-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="54ca0-155">Scorrere verso il basso `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour risorsa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="54ca0-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Navigare in Esplora risorse di Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="54ca0-157">*Componenti* è hello base risorse di Application Insights per la visualizzazione di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="54ca0-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="54ca0-158">Sono disponibili risorse separate per le regole di avviso e i test web disponibilità di hello associati.</span><span class="sxs-lookup"><span data-stu-id="54ca0-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="54ca0-159">Hello copia JSON del componente hello nella posizione appropriata hello in `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="54ca0-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="54ca0-160">Eliminare queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="54ca0-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="54ca0-161">Aprire le sezioni utilizzata e alertrules hello e copiare hello JSON per i singoli elementi nel modello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="54ca0-162">(Non la si copia da hello utilizzata o alertrules nodi: passare elementi hello sottostanti.)</span><span class="sxs-lookup"><span data-stu-id="54ca0-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="54ca0-163">Ciascun test web dispone di una regola di avviso associata, in modo che sia toocopy due di essi.</span><span class="sxs-lookup"><span data-stu-id="54ca0-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="54ca0-164">È possibile includere anche avvisi nelle metriche.</span><span class="sxs-lookup"><span data-stu-id="54ca0-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="54ca0-165">[Nomi delle metriche](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="54ca0-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="54ca0-166">Inserire questa riga in ciascuna risorsa:</span><span class="sxs-lookup"><span data-stu-id="54ca0-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="54ca0-167">Parametri di modello hello</span><span class="sxs-lookup"><span data-stu-id="54ca0-167">Parameterize hello template</span></span>
<span data-ttu-id="54ca0-168">Ora si dispone di nomi specifici di hello tooreplace con parametri.</span><span class="sxs-lookup"><span data-stu-id="54ca0-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="54ca0-169">troppo[un modello di parametrizzare](../azure-resource-manager/resource-group-authoring-templates.md), si scrivono espressioni utilizzando un [set di funzioni di supporto](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="54ca0-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="54ca0-170">Non è possibile parametrizzare solo una parte di una stringa, pertanto utilizzare `concat()` toobuild stringhe.</span><span class="sxs-lookup"><span data-stu-id="54ca0-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="54ca0-171">Ecco alcuni esempi di sostituzioni hello è opportuno toomake.</span><span class="sxs-lookup"><span data-stu-id="54ca0-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="54ca0-172">Sono presenti più occorrenze di ogni sostituzione.</span><span class="sxs-lookup"><span data-stu-id="54ca0-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="54ca0-173">Potrebbero esserne necessarie altre nel modello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-173">You might need others in your template.</span></span> <span data-ttu-id="54ca0-174">Questi esempi utilizzano parametri di hello e le variabili che sono definite nella parte superiore di hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="54ca0-175">find</span><span class="sxs-lookup"><span data-stu-id="54ca0-175">find</span></span> | <span data-ttu-id="54ca0-176">sostituire con</span><span class="sxs-lookup"><span data-stu-id="54ca0-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="54ca0-177">`"myappname"` (minuscolo)</span><span class="sxs-lookup"><span data-stu-id="54ca0-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="54ca0-178">Eliminare GUID e ID.</span><span class="sxs-lookup"><span data-stu-id="54ca0-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="54ca0-179">Set di dipendenze tra le risorse di hello</span><span class="sxs-lookup"><span data-stu-id="54ca0-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="54ca0-180">Azure è necessario impostare le risorse di hello in stretto ordine.</span><span class="sxs-lookup"><span data-stu-id="54ca0-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="54ca0-181">toomake che un programma di installazione venga completata prima di hello inizia successivamente, aggiungere righe di dipendenze:</span><span class="sxs-lookup"><span data-stu-id="54ca0-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="54ca0-182">La disponibilità di hello testare risorsa:</span><span class="sxs-lookup"><span data-stu-id="54ca0-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="54ca0-183">Nella risorsa di avviso hello per un test di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="54ca0-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="54ca0-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54ca0-184">Next steps</span></span>
<span data-ttu-id="54ca0-185">Altri articoli di automazione:</span><span class="sxs-lookup"><span data-stu-id="54ca0-185">Other automation articles:</span></span>

* <span data-ttu-id="54ca0-186">[Creare una risorsa di Application Insights](app-insights-powershell-script-create-resource.md) : metodo rapido che esclude l'uso di un modello.</span><span class="sxs-lookup"><span data-stu-id="54ca0-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="54ca0-187">Configurare avvisi</span><span class="sxs-lookup"><span data-stu-id="54ca0-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="54ca0-188">Creare test Web</span><span class="sxs-lookup"><span data-stu-id="54ca0-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="54ca0-189">Inviare informazioni di diagnostica Azure tooApplication</span><span class="sxs-lookup"><span data-stu-id="54ca0-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="54ca0-190">Distribuire tooAzure da GitHub</span><span class="sxs-lookup"><span data-stu-id="54ca0-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="54ca0-191">Creare annotazioni di rilascio</span><span class="sxs-lookup"><span data-stu-id="54ca0-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

