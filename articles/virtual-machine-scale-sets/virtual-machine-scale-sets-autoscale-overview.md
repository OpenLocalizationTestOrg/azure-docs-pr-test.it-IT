---
title: "Ridimensionamento automatico e set di scalabilità di macchine virtuali | Microsoft Docs"
description: "Informazioni sull'uso della diagnostica e delle risorse di scalabilità automatica per ridimensionare automaticamente le macchine virtuali in un set di scalabilità."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="cd177-103">Come usare ridimensionamento automatico e set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cd177-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="cd177-104">Il ridimensionamento automatico delle macchine virtuali in un set di scalabilità consiste nella creazione o nell'eliminazione di macchine nel set in base alle esigenze per soddisfare i requisiti a livello di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cd177-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="cd177-105">Man mano che aumenta il volume di lavoro, è possibile che un'applicazione richieda risorse aggiuntive per poter eseguire le attività in modo efficace.</span><span class="sxs-lookup"><span data-stu-id="cd177-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="cd177-106">Il ridimensionamento automatico è un processo automatico che semplifica il sovraccarico di gestione.</span><span class="sxs-lookup"><span data-stu-id="cd177-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="cd177-107">Riducendo il sovraccarico, non è necessario monitorare le prestazioni del sistema continuamente o decidere come gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="cd177-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="cd177-108">Il ridimensionamento è un processo elastico.</span><span class="sxs-lookup"><span data-stu-id="cd177-108">Scaling is an elastic process.</span></span> <span data-ttu-id="cd177-109">Con l'aumentare del carico è possibile aggiungere altre risorse</span><span class="sxs-lookup"><span data-stu-id="cd177-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="cd177-110">e, man mano che la richiesta diminuisce, le risorse possono essere rimosse per ridurre al minimo i costi e mantenere i livelli di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cd177-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="cd177-111">Configurare il ridimensionamento automatico di un set di scalabilità tramite un modello di Azure Resource Manager, usando Azure PowerShell, l'interfaccia della riga di comando di Azure o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd177-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="cd177-112">Configurare il ridimensionamento usando modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd177-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="cd177-113">Invece di distribuire e gestire separatamente ogni risorsa dell'applicazione, usare un modello che distribuisce tutte le risorse in un'unica operazione coordinata.</span><span class="sxs-lookup"><span data-stu-id="cd177-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="cd177-114">Nel modello vengono definite le risorse dell'applicazione e vengono specificati i parametri di distribuzione per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="cd177-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="cd177-115">Il modello è composto da JSON ed espressioni che è possibile usare per creare valori per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cd177-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="cd177-116">Per altre informazioni, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cd177-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="cd177-117">Nel modello si specifica l'elemento capacità:</span><span class="sxs-lookup"><span data-stu-id="cd177-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="cd177-118">La capacità identifica il numero di macchine virtuali nel set.</span><span class="sxs-lookup"><span data-stu-id="cd177-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="cd177-119">È possibile modificare manualmente la capacità distribuendo un modello con un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="cd177-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="cd177-120">Se si distribuisce un modello per modificare solo la capacità, è possibile includere solo l'elemento SKU con la capacità aggiornata.</span><span class="sxs-lookup"><span data-stu-id="cd177-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="cd177-121">La capacità del set di scalabilità può essere regolata automaticamente usando una combinazione della risorsa **autoscaleSettings** e dell'estensione Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="cd177-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="cd177-122">Configurare l'estensione Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="cd177-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="cd177-123">Il ridimensionamento automatico può essere eseguito solo se la raccolta di metriche è riuscita in ogni macchina virtuale del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cd177-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="cd177-124">L'estensione Diagnostica di Azure fornisce le funzionalità di monitoraggio e diagnostica che soddisfano le esigenze di raccolta delle metriche della risorsa di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="cd177-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="cd177-125">È possibile installare l'estensione come parte del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd177-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="cd177-126">Questo esempio mostra le variabili usate nel modello per configurare l'estensione di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="cd177-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="cd177-127">I parametri vengono forniti quando si distribuisce il modello.</span><span class="sxs-lookup"><span data-stu-id="cd177-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="cd177-128">In questo esempio vengono forniti il nome dell'account di archiviazione, in cui vengono archiviati i dati, e il nome del set di scalabilità, in cui vengono raccolti i dati.</span><span class="sxs-lookup"><span data-stu-id="cd177-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="cd177-129">Anche in questo esempio di Windows Server vengono raccolti solo i dati del contatore delle prestazioni Conteggio dei thread.</span><span class="sxs-lookup"><span data-stu-id="cd177-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="cd177-130">Tutti i contatori delle prestazioni disponibili in Windows o Linux possono essere usati per raccogliere informazioni di diagnostica e possono essere inclusi nella configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="cd177-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="cd177-131">Questo esempio illustra la definizione dell'estensione nel modello:</span><span class="sxs-lookup"><span data-stu-id="cd177-131">This example shows the definition of the extension in the template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="cd177-132">Quando viene eseguita l'estensione Diagnostica, i dati vengono archiviati e raccolti in una tabella, nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="cd177-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="cd177-133">I dati raccolti sono disponibili nella tabella **WADPerformanceCounters**:</span><span class="sxs-lookup"><span data-stu-id="cd177-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="cd177-134">Configurare la risorsa autoScaleSettings</span><span class="sxs-lookup"><span data-stu-id="cd177-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="cd177-135">La risorsa autoscaleSettings usa le informazioni raccolte dall'estensione di Diagnostica per prendere decisioni sull'aumento o la riduzione del numero di macchine virtuali nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cd177-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="cd177-136">Questo esempio illustra la configurazione della risorsa nel modello:</span><span class="sxs-lookup"><span data-stu-id="cd177-136">This example shows the configuration of the resource in the template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="cd177-137">Nell'esempio precedente vengono create due regole per definire le azioni di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="cd177-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="cd177-138">La prima regola definisce l'azione di aumento delle istanze e la seconda regola definisce l'azione di riduzione del numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="cd177-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="cd177-139">Questi valori vengono forniti nelle regole:</span><span class="sxs-lookup"><span data-stu-id="cd177-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="cd177-140">Regola</span><span class="sxs-lookup"><span data-stu-id="cd177-140">Rule</span></span> | <span data-ttu-id="cd177-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cd177-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="cd177-142">metricName</span><span class="sxs-lookup"><span data-stu-id="cd177-142">metricName</span></span>        | <span data-ttu-id="cd177-143">Questo valore corrisponde al contatore delle prestazioni definito nella variabile wadperfcounter per l'estensione Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="cd177-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="cd177-144">Nell'esempio precedente viene usato il contatore Conteggio dei thread.</span><span class="sxs-lookup"><span data-stu-id="cd177-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="cd177-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="cd177-145">metricResourceUri</span></span> | <span data-ttu-id="cd177-146">Questo valore è l'identificatore di risorsa del set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cd177-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="cd177-147">Questo identificatore contiene il nome del gruppo di risorse, il nome del provider di risorse e il nome del set di scalabilità per il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cd177-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="cd177-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="cd177-148">timeGrain</span></span>         | <span data-ttu-id="cd177-149">Questo valore corrisponde alla granularità delle metriche che vengono raccolte.</span><span class="sxs-lookup"><span data-stu-id="cd177-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="cd177-150">Nell'esempio precedente i dati vengono raccolti con un intervallo di un minuto.</span><span class="sxs-lookup"><span data-stu-id="cd177-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="cd177-151">Questo valore viene usato con timeWindow.</span><span class="sxs-lookup"><span data-stu-id="cd177-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="cd177-152">statistic</span><span class="sxs-lookup"><span data-stu-id="cd177-152">statistic</span></span>         | <span data-ttu-id="cd177-153">Questo valore determina il modo in cui vengono combinate le metriche per consentire l'azione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="cd177-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="cd177-154">I valori possibili sono: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="cd177-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="cd177-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="cd177-155">timeWindow</span></span>        | <span data-ttu-id="cd177-156">Questo valore rappresenta l'intervallo di tempo in cui vengono raccolti i dati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="cd177-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="cd177-157">Deve essere compreso tra 5 minuti e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="cd177-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="cd177-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="cd177-158">timeAggregation</span></span>   | <span data-ttu-id="cd177-159">Questo valore definisce il modo in cui i dati raccolti devono essere combinati nel tempo.</span><span class="sxs-lookup"><span data-stu-id="cd177-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="cd177-160">Il valore predefinito è "Average".</span><span class="sxs-lookup"><span data-stu-id="cd177-160">The default value is Average.</span></span> <span data-ttu-id="cd177-161">I valori possibili sono: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="cd177-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="cd177-162">operator</span><span class="sxs-lookup"><span data-stu-id="cd177-162">operator</span></span>          | <span data-ttu-id="cd177-163">Questo valore indica l'operatore usato per confrontare i dati della metrica e la soglia.</span><span class="sxs-lookup"><span data-stu-id="cd177-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="cd177-164">I valori possibili sono: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="cd177-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="cd177-165">threshold</span><span class="sxs-lookup"><span data-stu-id="cd177-165">threshold</span></span>         | <span data-ttu-id="cd177-166">Questo valore indica l'attivazione dell'azione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cd177-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="cd177-167">Assicurarsi di fornire una differenza sufficiente tra i valori delle soglie per le azioni di **aumento delle istanze** e di **riduzione delle istanze**.</span><span class="sxs-lookup"><span data-stu-id="cd177-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="cd177-168">Se si impostano gli stessi valori per entrambe le azioni, il sistema prevede un'evoluzione costante che impedisce l'implementazione di un'azione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cd177-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="cd177-169">Ad esempio, impostando entrambi i valori su 600 thread, l'esempio precedente non funziona.</span><span class="sxs-lookup"><span data-stu-id="cd177-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="cd177-170">direction</span><span class="sxs-lookup"><span data-stu-id="cd177-170">direction</span></span>         | <span data-ttu-id="cd177-171">Questo valore determina l'azione da eseguire quando viene raggiunto il valore di soglia.</span><span class="sxs-lookup"><span data-stu-id="cd177-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="cd177-172">I valori possibili sono Increase o Decrease.</span><span class="sxs-lookup"><span data-stu-id="cd177-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="cd177-173">type</span><span class="sxs-lookup"><span data-stu-id="cd177-173">type</span></span>              | <span data-ttu-id="cd177-174">Questo valore indica il tipo di azione che deve verificarsi e deve essere impostato su ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="cd177-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="cd177-175">value</span><span class="sxs-lookup"><span data-stu-id="cd177-175">value</span></span>             | <span data-ttu-id="cd177-176">Questo valore indica il numero di macchine virtuali che vengono aggiunte o rimosse dal set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cd177-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="cd177-177">Questo valore deve essere uguale o maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="cd177-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="cd177-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="cd177-178">cooldown</span></span>          | <span data-ttu-id="cd177-179">Questo valore indica il tempo di attesa dopo l'ultima azione di ridimensionamento prima che venga eseguita l'azione successiva.</span><span class="sxs-lookup"><span data-stu-id="cd177-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="cd177-180">Questo valore deve essere compreso tra un minuto e una settimana.</span><span class="sxs-lookup"><span data-stu-id="cd177-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="cd177-181">A seconda del contatore delle prestazioni scelto, alcuni elementi della configurazione del modello vengono usati in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="cd177-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="cd177-182">Nell'esempio precedente, il contatore delle prestazioni è Conteggio dei thread e il valore di soglia è impostato su 650 per un'azione di aumento delle istanze e su 550 per l'azione di riduzione delle istanze.</span><span class="sxs-lookup"><span data-stu-id="cd177-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="cd177-183">Se si usa un contatore come%Processor Time, il valore di soglia è impostato sulla percentuale di utilizzo della CPU che determina un'azione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="cd177-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="cd177-184">Quando viene attivata un'azione di ridimensionamento, ad esempio un carico elevato, la capacità del set viene aumentata in base al valore presente nel modello.</span><span class="sxs-lookup"><span data-stu-id="cd177-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="cd177-185">Ad esempio, in un set di scalabilità in cui la capacità è impostata su 3 e il valore dell'azione di ridimensionamento è impostato su 1:</span><span class="sxs-lookup"><span data-stu-id="cd177-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="cd177-186">Quando viene il carico corrente causa il superamento della soglia di 650 del conteggio medio dei thread:</span><span class="sxs-lookup"><span data-stu-id="cd177-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="cd177-187">Viene attivata un'azione di **aumento delle istanze** a causa della quale la capacità del set viene aumentata di uno:</span><span class="sxs-lookup"><span data-stu-id="cd177-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="cd177-188">Come conseguenza una macchina virtuale viene aggiunta al set di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="cd177-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="cd177-189">Dopo un periodo di attesa di cinque minuti, se il numero medio di thread nelle macchine virtuali rimane oltre 600, viene aggiunta un'altra macchina virtuale al set.</span><span class="sxs-lookup"><span data-stu-id="cd177-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="cd177-190">Se il numero medio di thread rimane sotto 550, la capacità del set di scalabilità viene ridotta di uno e una macchina virtuale viene rimossa dal set.</span><span class="sxs-lookup"><span data-stu-id="cd177-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="cd177-191">Impostare la scalabilità con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd177-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="cd177-192">Per visualizzare esempi d'uso di PowerShell per configurare il ridimensionamento automatico, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="cd177-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="cd177-193">Impostare la scalabilità con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="cd177-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="cd177-194">Per visualizzare esempi d'uso dell'interfaccia della riga di comando di Azure per configurare il ridimensionamento automatico, vedere [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md) (Esempi di avvio rapido dell'interfaccia della riga di comando multipiattaforma per Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="cd177-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="cd177-195">Impostare il ridimensionamento con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cd177-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="cd177-196">Per visualizzare un esempio d'uso del portale di Azure per impostare il ridimensionamento automatico, vedere [Creare un set di scalabilità di macchine virtuali tramite il portale di Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="cd177-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="cd177-197">Analisi delle azioni di ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="cd177-197">Investigate scaling actions</span></span>

* <span data-ttu-id="cd177-198">**Portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="cd177-198">**Azure portal**</span></span>  
<span data-ttu-id="cd177-199">Attualmente è possibile ottenere una quantità limitata di informazioni tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="cd177-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="cd177-200">**Esplora risorse di Azure**</span><span class="sxs-lookup"><span data-stu-id="cd177-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="cd177-201">Si tratta dello strumento migliore per esaminare lo stato corrente del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cd177-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="cd177-202">Seguire questo percorso per passare alla visualizzazione dell'istanza del set di scalabilità creato:</span><span class="sxs-lookup"><span data-stu-id="cd177-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="cd177-203">**Subscriptions > {sottoscrizione dell'utente} > resourceGroups > {gruppo di risorse dell'utente} > providers > Microsoft.Compute > virtualMachineScaleSets > {set di scalabilità dell'utente} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="cd177-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="cd177-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cd177-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="cd177-205">Usare questo comando per ottenere alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="cd177-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="cd177-206">Connettersi alla macchina virtuale jumpbox esattamente come a qualsiasi altra macchina virtuale e quindi accedere in modalità remota alle macchine virtuali nel set di scalabilità per monitorare i singoli processi.</span><span class="sxs-lookup"><span data-stu-id="cd177-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd177-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd177-207">Next Steps</span></span>
* <span data-ttu-id="cd177-208">Per un esempio sulla modalità di creazione di un set di scalabilità configurando il ridimensionamento automatico, vedere [Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali](virtual-machine-scale-sets-windows-autoscale.md) .</span><span class="sxs-lookup"><span data-stu-id="cd177-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="cd177-209">Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="cd177-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="cd177-210">Per informazioni sulle funzionalità di notifica, vedere [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md) (Usare le azioni di ridimensionamento automatico per inviare notifiche di avviso di webhook ed e-mail in Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="cd177-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="cd177-211">Per informazioni, vedere [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md) (Usare i log di controllo per inviare notifiche di avviso di webhook in Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="cd177-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="cd177-212">Informazioni sugli [scenari di scalabilità automatica avanzata](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="cd177-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
