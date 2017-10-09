---
title: aaaProvision un'app web che utilizza un Database SQL
description: Utilizzare un toodeploy di modello un'app web che include un Database SQL di Azure Resource Manager.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: fb9648e1-9bf2-4537-bc4a-ab8d4953168c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 189c0122d201e88f15013bf241d66652ef23df4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-web-app-with-a-sql-database"></a><span data-ttu-id="5c024-103">Eseguire il provisioning di un'app Web con un database SQL</span><span class="sxs-lookup"><span data-stu-id="5c024-103">Provision a web app with a SQL Database</span></span>
<span data-ttu-id="5c024-104">In questo argomento si apprenderà come toocreate un modello di gestione risorse di Azure che consente di distribuire un'app web e il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="5c024-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app and SQL Database.</span></span> <span data-ttu-id="5c024-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5c024-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="5c024-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="5c024-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5c024-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5c024-108">Per altre informazioni sulla distribuzione di app, vedere [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="5c024-108">For more information about deploying apps, see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="5c024-109">Per il modello di hello completo, vedere [modello App Web con Database SQL](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="5c024-109">For hello complete template, see [Web App With SQL Database template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="5c024-110">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="5c024-110">What you will deploy</span></span>
<span data-ttu-id="5c024-111">In questo modello, verrà distribuito quanto segue:</span><span class="sxs-lookup"><span data-stu-id="5c024-111">In this template, you will deploy:</span></span>

* <span data-ttu-id="5c024-112">Un'app Web</span><span class="sxs-lookup"><span data-stu-id="5c024-112">a web app</span></span>
* <span data-ttu-id="5c024-113">Server di database SQL</span><span class="sxs-lookup"><span data-stu-id="5c024-113">SQL Database server</span></span>
* <span data-ttu-id="5c024-114">Database SQL</span><span class="sxs-lookup"><span data-stu-id="5c024-114">SQL Database</span></span>
* <span data-ttu-id="5c024-115">Impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="5c024-115">AutoScale settings</span></span>
* <span data-ttu-id="5c024-116">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="5c024-116">Alert rules</span></span>
* <span data-ttu-id="5c024-117">Informazioni sull'app</span><span class="sxs-lookup"><span data-stu-id="5c024-117">App Insights</span></span>

<span data-ttu-id="5c024-118">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="5c024-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5c024-119">[![Distribuire tooAzure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5c024-119">[![Deploy tooAzure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="5c024-120">I parametri toospecify</span><span class="sxs-lookup"><span data-stu-id="5c024-120">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="administratorlogin"></a><span data-ttu-id="5c024-121">administratorLogin</span><span class="sxs-lookup"><span data-stu-id="5c024-121">administratorLogin</span></span>
<span data-ttu-id="5c024-122">Hello toouse nome account dell'amministratore di server di database hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-122">hello account name toouse for hello database server administrator.</span></span>

    "administratorLogin": {
      "type": "string"
    }

### <a name="administratorloginpassword"></a><span data-ttu-id="5c024-123">administratorLoginPassword</span><span class="sxs-lookup"><span data-stu-id="5c024-123">administratorLoginPassword</span></span>
<span data-ttu-id="5c024-124">Hello toouse password dell'amministratore di server di database hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-124">hello password toouse for hello database server administrator.</span></span>

    "administratorLoginPassword": {
      "type": "securestring"
    }

### <a name="databasename"></a><span data-ttu-id="5c024-125">databaseName</span><span class="sxs-lookup"><span data-stu-id="5c024-125">databaseName</span></span>
<span data-ttu-id="5c024-126">nome Hello di hello nuovo database toocreate.</span><span class="sxs-lookup"><span data-stu-id="5c024-126">hello name of hello new database toocreate.</span></span>

    "databaseName": {
      "type": "string",
      "defaultValue": "sampledb"
    }

### <a name="collation"></a><span data-ttu-id="5c024-127">collation</span><span class="sxs-lookup"><span data-stu-id="5c024-127">collation</span></span>
<span data-ttu-id="5c024-128">toouse di regole di confronto database Hello per hello che controllano corretto utilizzo di caratteri.</span><span class="sxs-lookup"><span data-stu-id="5c024-128">hello database collation toouse for governing hello proper use of characters.</span></span>

    "collation": {
      "type": "string",
      "defaultValue": "SQL_Latin1_General_CP1_CI_AS"
    }

### <a name="edition"></a><span data-ttu-id="5c024-129">edition</span><span class="sxs-lookup"><span data-stu-id="5c024-129">edition</span></span>
<span data-ttu-id="5c024-130">tipo di Hello di toocreate di database.</span><span class="sxs-lookup"><span data-stu-id="5c024-130">hello type of database toocreate.</span></span>

    "edition": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "Standard",
        "Premium"
      ],
      "metadata": {
        "description": "hello type of database toocreate."
      }
    }

### <a name="maxsizebytes"></a><span data-ttu-id="5c024-131">maxSizeBytes</span><span class="sxs-lookup"><span data-stu-id="5c024-131">maxSizeBytes</span></span>
<span data-ttu-id="5c024-132">dimensione massima Hello, in byte, per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-132">hello maximum size, in bytes, for hello database.</span></span>

    "maxSizeBytes": {
      "type": "string",
      "defaultValue": "1073741824"
    }

### <a name="requestedserviceobjectivename"></a><span data-ttu-id="5c024-133">requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="5c024-133">requestedServiceObjectiveName</span></span>
<span data-ttu-id="5c024-134">Hello nome corrispondente toohello livello di prestazioni per l'edizione.</span><span class="sxs-lookup"><span data-stu-id="5c024-134">hello name corresponding toohello performance level for edition.</span></span> 

    "requestedServiceObjectiveName": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "S0",
        "S1",
        "S2",
        "P1",
        "P2",
        "P3"
      ],
      "metadata": {
        "description": "Describes hello performance level for Edition"
      }
    }

## <a name="variables-for-names"></a><span data-ttu-id="5c024-135">Variabili per i nomi</span><span class="sxs-lookup"><span data-stu-id="5c024-135">Variables for names</span></span>
<span data-ttu-id="5c024-136">Questo modello include variabili di costruire nomi utilizzati nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-136">This template includes variables that construct names used in hello template.</span></span> <span data-ttu-id="5c024-137">i valori delle variabili Hello utilizzano hello **uniqueString** funzione toogenerate un nome da id gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-137">hello variable values use hello **uniqueString** function toogenerate a name from hello resource group id.</span></span>

    "variables": {
        "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
        "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
        "sqlserverName": "[concat('sqlserver', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="5c024-138">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="5c024-138">Resources toodeploy</span></span>
### <a name="sql-server-and-database"></a><span data-ttu-id="5c024-139">Database e server SQL</span><span class="sxs-lookup"><span data-stu-id="5c024-139">SQL Server and Database</span></span>
<span data-ttu-id="5c024-140">Crea un nuovo database e server SQL.</span><span class="sxs-lookup"><span data-stu-id="5c024-140">Creates a new SQL Server and database.</span></span> <span data-ttu-id="5c024-141">nome Hello del server hello è specificato in hello **serverName** parametro e hello posizione specificata in hello **serverLocation** parametro.</span><span class="sxs-lookup"><span data-stu-id="5c024-141">hello name of hello server is specified in hello **serverName** parameter and hello location specified in hello **serverLocation** parameter.</span></span> <span data-ttu-id="5c024-142">Quando si crea il nuovo server di hello, è necessario fornire un nome di accesso e una password per l'amministratore del server database hello.</span><span class="sxs-lookup"><span data-stu-id="5c024-142">When creating hello new server, you must provide a login name and password for hello database server administrator.</span></span> 

    {
      "name": "[variables('sqlserverName')]",
      "type": "Microsoft.Sql/servers",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "SqlServer"
      },
      "apiVersion": "2014-04-01-preview",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "name": "[parameters('databaseName')]",
          "type": "databases",
          "location": "[resourceGroup().location]",
          "tags": {
            "displayName": "Database"
          },
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "properties": {
            "edition": "[parameters('edition')]",
            "collation": "[parameters('collation')]",
            "maxSizeBytes": "[parameters('maxSizeBytes')]",
            "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
          }
        },
        {
          "type": "firewallrules",
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "location": "[resourceGroup().location]",
          "name": "AllowAllAzureIps",
          "properties": {
            "endIpAddress": "0.0.0.0",
            "startIpAddress": "0.0.0.0"
          }
        }
      ]
    },

[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="5c024-143">App Web</span><span class="sxs-lookup"><span data-stu-id="5c024-143">Web app</span></span>
    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "connectionstrings",
          "dependsOn": [
            "[variables('webSiteName')]"
          ],
          "properties": {
            "DefaultConnection": {
              "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', variables('sqlserverName'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('databaseName'), ';User Id=', parameters('administratorLogin'), '@', variables('sqlserverName'), ';Password=', parameters('administratorLoginPassword'), ';')]",
              "type": "SQLServer"
            }
          }
        }
      ]
    },


### <a name="autoscale"></a><span data-ttu-id="5c024-144">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="5c024-144">AutoScale</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
      "type": "Microsoft.Insights/autoscalesettings",
      "location": "[resourceGroup().location]",
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "properties": {
        "profiles": [
          {
            "name": "Default",
            "capacity": {
              "minimum": 1,
              "maximum": 2,
              "default": 1
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT10M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 80.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT10M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT1H",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60.0
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT1H"
                }
              }
            ]
          }
        ],
        "enabled": false,
        "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
        "targetResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      }
    },


### <a name="alert-rules-for-status-codes-403-and-500s-high-cpu-and-http-queue-length"></a><span data-ttu-id="5c024-145">Regole di avviso per i codici di stato 403 e 500, Utilizzo CPU elevato e Lunghezza coda HTTP</span><span class="sxs-lookup"><span data-stu-id="5c024-145">Alert rules for status codes 403 and 500's, High CPU, and HTTP Queue Length</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ServerErrors ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ServerErrorsAlertRule"
      },
      "properties": {
        "name": "[concat('ServerErrors ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some server errors, status code 5xx.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http5xx"
          },
          "operator": "GreaterThan",
          "threshold": 0.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ForbiddenRequestsAlertRule"
      },
      "properties": {
        "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some requests that are forbidden, status code 403.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http403"
          },
          "operator": "GreaterThan",
          "threshold": 0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "CPUHighAlertRule"
      },
      "properties": {
        "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
        "description": "[concat('hello average CPU is high across all hello instances of ', variables('hostingPlanName'))]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
            "metricName": "CpuPercentage"
          },
          "operator": "GreaterThan",
          "threshold": 90,
          "windowSize": "PT15M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "properties": {
        "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
        "description": "[concat('hello HTTP queue for hello instances of ', variables('hostingPlanName'), ' has a large number of pending requests.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]",
            "metricName": "HttpQueueLength"
          },
          "operator": "GreaterThan",
          "threshold": 100.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },

### <a name="app-insights"></a><span data-ttu-id="5c024-146">Informazioni sull'app</span><span class="sxs-lookup"><span data-stu-id="5c024-146">App Insights</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('AppInsights', variables('webSiteName'))]",
      "type": "Microsoft.Insights/components",
      "location": "Central US",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "AppInsightsComponent"
      },
      "properties": {
        "ApplicationId": "[variables('webSiteName')]"
      }
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5c024-147">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="5c024-147">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="5c024-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c024-148">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli"></a><span data-ttu-id="5c024-149">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5c024-149">Azure CLI</span></span>

    azure config mode arm
    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="5c024-150">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5c024-150">Azure CLI 2.0</span></span>

    az resource deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE]
> <span data-ttu-id="5c024-151">Per il contenuto del file JSON di hello parametri, vedere [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="5c024-151">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span></span>
>
>
