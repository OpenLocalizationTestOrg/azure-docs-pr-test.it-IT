---
title: "set di scalabilità aaaAutomatic scalabilità e la macchina virtuale | Documenti Microsoft"
description: "Informazioni sull'utilizzo di diagnostica e le macchine virtuali di scalabilità automatica risorse tooautomatically scala in un set di scalabilità."
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="5a205-103">Come il ridimensionamento automatico toouse e set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5a205-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5a205-104">Il ridimensionamento automatico delle macchine virtuali in un set di scalabilità è la creazione di hello o l'eliminazione delle macchine in hello impostato come necessarie toomatch requisiti relativi alle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5a205-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="5a205-105">Man mano che aumenta il volume di hello di lavoro, un'applicazione può richiedere risorse aggiuntive tooenable è tooeffectively eseguire attività.</span><span class="sxs-lookup"><span data-stu-id="5a205-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="5a205-106">Il ridimensionamento automatico è un processo automatico che semplifica il sovraccarico di gestione.</span><span class="sxs-lookup"><span data-stu-id="5a205-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="5a205-107">Riducendo il sovraccarico non necessario toocontinually monitoraggio delle prestazioni di sistema o decidere come toomanage risorse.</span><span class="sxs-lookup"><span data-stu-id="5a205-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="5a205-108">Il ridimensionamento è un processo elastico.</span><span class="sxs-lookup"><span data-stu-id="5a205-108">Scaling is an elastic process.</span></span> <span data-ttu-id="5a205-109">Altre risorse possono essere aggiunti come hello carico aumenta.</span><span class="sxs-lookup"><span data-stu-id="5a205-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="5a205-110">E come richiesta diminuisce, le risorse possono essere rimossi toominimize costi e mantenere livelli di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="5a205-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="5a205-111">Impostare la scalabilità automatica su una scala impostata per l'utilizzo di un modello Gestione risorse di Azure, Azure PowerShell, CLI di Azure o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a205-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="5a205-112">Configurare il ridimensionamento usando modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5a205-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="5a205-113">Invece di distribuire e gestire separatamente ogni risorsa dell'applicazione, usare un modello che distribuisce tutte le risorse in un'unica operazione coordinata.</span><span class="sxs-lookup"><span data-stu-id="5a205-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="5a205-114">Nel modello di hello, le risorse dell'applicazione sono definite e vengono specificati i parametri di distribuzione per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="5a205-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="5a205-115">modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5a205-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="5a205-116">toolearn esaminare più, [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5a205-117">Nel modello di hello, specificare l'elemento capacità hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="5a205-118">Capacità identifica il numero di hello di macchine virtuali nel set di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="5a205-119">È possibile modificare manualmente la capacità di hello tramite la distribuzione di un modello con un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="5a205-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="5a205-120">Se si distribuisce una capacità di hello modifica tooonly modello, è possibile includere solo elemento SKU hello con capacità di hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="5a205-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="5a205-121">Hello capacità del set di scala possono essere adattate automaticamente usando una combinazione di hello **autoscaleSettings** risorsa e hello estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="5a205-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="5a205-122">Configurare l'estensione diagnostica di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5a205-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="5a205-123">La scalabilità automatica può essere eseguita solo se la raccolta di metriche ha esito positivo in ogni macchina virtuale nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="5a205-124">Hello estensione diagnostica di Azure offre funzionalità di monitoraggio e diagnostica di hello soddisfa le esigenze di raccolta metriche hello della risorsa di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="5a205-125">È possibile installare l'estensione hello come parte del modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="5a205-126">Questo esempio mostra le variabili di hello utilizzate nell'estensione di diagnostica di hello modello tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="5a205-127">I parametri vengono forniti quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="5a205-128">In questo esempio, il nome di hello dell'account di archiviazione hello (dove vengono archiviati dati) e hello vengono forniti nome del set di scalabilità hello (in cui vengono raccolti dati).</span><span class="sxs-lookup"><span data-stu-id="5a205-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="5a205-129">Anche in questo esempio di Windows Server, verrà raccolti solo contatore delle prestazioni conteggio Thread hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="5a205-130">Tutti hello contatori delle prestazioni disponibili in Windows o Linux possono essere utilizzati toocollect informazioni di diagnostica e possono essere inclusi nella configurazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="5a205-131">Questo esempio mostra la definizione hello dell'estensione hello nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="5a205-132">Quando viene eseguita l'estensione di diagnostica hello, dati hello archiviati e raccolti in una tabella, nell'account di archiviazione hello specificato.</span><span class="sxs-lookup"><span data-stu-id="5a205-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="5a205-133">In hello **WADPerformanceCounters** tabella, è possibile trovare i dati raccolti hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="5a205-134">La configurazione di risorsa autoScaleSettings hello</span><span class="sxs-lookup"><span data-stu-id="5a205-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="5a205-135">risorsa autoscaleSettings Hello utilizza informazioni hello hello diagnostica estensione toodecide se tooincrease o diminuire il numero di hello delle macchine virtuali in scala di hello impostata.</span><span class="sxs-lookup"><span data-stu-id="5a205-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="5a205-136">Questo esempio mostra la configurazione hello della risorsa hello nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="5a205-137">Nell'esempio hello sopra, vengono create due regole per la definizione di azioni di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="5a205-138">prima regola Hello definisce l'azione di scalabilità orizzontale hello e regola secondo hello hello scala-azione.</span><span class="sxs-lookup"><span data-stu-id="5a205-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="5a205-139">Questi valori sono disponibili nelle regole di hello:</span><span class="sxs-lookup"><span data-stu-id="5a205-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="5a205-140">Regola</span><span class="sxs-lookup"><span data-stu-id="5a205-140">Rule</span></span> | <span data-ttu-id="5a205-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5a205-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="5a205-142">metricName</span><span class="sxs-lookup"><span data-stu-id="5a205-142">metricName</span></span>        | <span data-ttu-id="5a205-143">Questo valore è hello stesso come contatore delle prestazioni hello che siano definiti nella variabile wadperfcounter hello per l'estensione diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="5a205-144">Nell'esempio hello sopra, il contatore di conteggio Thread hello è utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5a205-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="5a205-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="5a205-145">metricResourceUri</span></span> | <span data-ttu-id="5a205-146">Questo valore è l'identificatore di risorsa hello del set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="5a205-147">Questo identificatore contiene nome hello hello del gruppo di risorse, hello nome del provider di risorse hello e nome hello di hello scala set tooscale.</span><span class="sxs-lookup"><span data-stu-id="5a205-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="5a205-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="5a205-148">timeGrain</span></span>         | <span data-ttu-id="5a205-149">Questo valore è la granularità hello di metriche di hello che vengono raccolti.</span><span class="sxs-lookup"><span data-stu-id="5a205-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="5a205-150">In hello sopra riportato, i dati vengono raccolti in un intervallo di un minuto.</span><span class="sxs-lookup"><span data-stu-id="5a205-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="5a205-151">Questo valore viene usato con timeWindow.</span><span class="sxs-lookup"><span data-stu-id="5a205-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="5a205-152">statistic</span><span class="sxs-lookup"><span data-stu-id="5a205-152">statistic</span></span>         | <span data-ttu-id="5a205-153">Questo valore determina come le metriche hello vengono combinati tooaccommodate hello azione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="5a205-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="5a205-154">Hello i valori possibili sono: Media, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="5a205-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="5a205-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="5a205-155">timeWindow</span></span>        | <span data-ttu-id="5a205-156">Questo valore è hello intervallo di tempo in cui vengono raccolti i dati dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="5a205-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="5a205-157">Deve essere compreso tra 5 minuti e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="5a205-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="5a205-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="5a205-158">timeAggregation</span></span>   | <span data-ttu-id="5a205-159">Questo valore determina la modalità hello i dati raccolti devono essere combinati nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5a205-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="5a205-160">valore predefinito di Hello è Media.</span><span class="sxs-lookup"><span data-stu-id="5a205-160">hello default value is Average.</span></span> <span data-ttu-id="5a205-161">Hello i valori possibili sono: Media, minimo, massimo, ultimo, totale, conteggio.</span><span class="sxs-lookup"><span data-stu-id="5a205-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="5a205-162">operator</span><span class="sxs-lookup"><span data-stu-id="5a205-162">operator</span></span>          | <span data-ttu-id="5a205-163">Questo valore è l'operatore hello toocompare utilizzati hello metrica hello e dati soglia.</span><span class="sxs-lookup"><span data-stu-id="5a205-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="5a205-164">Hello i valori possibili sono: uguale a, diverso da, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="5a205-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="5a205-165">threshold</span><span class="sxs-lookup"><span data-stu-id="5a205-165">threshold</span></span>         | <span data-ttu-id="5a205-166">Questo valore è hello che attiva l'azione di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="5a205-167">Essere tooprovide che una differenza tra valori di soglia hello per hello sufficiente **scalabilità orizzontale** e **scala aggiuntivo** azioni.</span><span class="sxs-lookup"><span data-stu-id="5a205-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="5a205-168">Se si impostano hello stessi valori per entrambe le azioni, il sistema hello prevede costante evoluzione, che ne impedisce l'implementazione di un'azione di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="5a205-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="5a205-169">Ad esempio, l'impostazione entrambi too600 i thread nel precedente esempio hello non funziona.</span><span class="sxs-lookup"><span data-stu-id="5a205-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="5a205-170">direction</span><span class="sxs-lookup"><span data-stu-id="5a205-170">direction</span></span>         | <span data-ttu-id="5a205-171">Questo valore determina l'azione eseguita quando viene raggiunto il valore di soglia hello hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="5a205-172">i valori possibili di Hello sono aumentano o diminuiscono.</span><span class="sxs-lookup"><span data-stu-id="5a205-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="5a205-173">type</span><span class="sxs-lookup"><span data-stu-id="5a205-173">type</span></span>              | <span data-ttu-id="5a205-174">Questo valore è di tipo hello di azione che deve essere eseguita e deve essere impostato tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="5a205-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="5a205-175">value</span><span class="sxs-lookup"><span data-stu-id="5a205-175">value</span></span>             | <span data-ttu-id="5a205-176">Questo valore è il numero di hello di macchine virtuali che vengono aggiunti tooor rimosso dal set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="5a205-177">Questo valore deve essere uguale o maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="5a205-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="5a205-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="5a205-178">cooldown</span></span>          | <span data-ttu-id="5a205-179">Questo valore è quantità hello di toowait tempo dall'ultima azione di scalabilità hello prima che si verifichi l'azione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="5a205-180">Questo valore deve essere compreso tra un minuto e una settimana.</span><span class="sxs-lookup"><span data-stu-id="5a205-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="5a205-181">A seconda del contatore delle prestazioni di hello, si utilizza, alcuni degli elementi di hello nella configurazione del modello hello vengono utilizzati in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="5a205-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="5a205-182">In hello sopra riportato, contatore delle prestazioni hello è il conteggio Thread, il valore di soglia hello è 650 per un'azione di scalabilità orizzontale e il valore di soglia hello è 550 per azione di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="5a205-183">Se si utilizza un contatore, ad esempio % tempo processore, il valore di soglia hello è toohello percentuale di utilizzo della CPU che determinano un'azione di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="5a205-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="5a205-184">Quando viene attivata un'azione di scalabilità, ad esempio un carico elevato, hello del set di hello viene aumentata in base a valore hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="5a205-185">Ad esempio, in una scala imposta in capacità hello è impostata too3 e hello scala azione è impostato too1:</span><span class="sxs-lookup"><span data-stu-id="5a205-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="5a205-186">Hello quando la corrente parte delle thread medio hello degli cause carico conteggio toogo superiore alla soglia hello di 650:</span><span class="sxs-lookup"><span data-stu-id="5a205-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="5a205-187">Oggetto **scalabilità orizzontale** viene attivata l'azione che causa hello capacità di hello set toobe incrementato di uno:</span><span class="sxs-lookup"><span data-stu-id="5a205-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="5a205-188">il risultato di Hello è che una macchina virtuale viene aggiunto il set di scalabilità toohello:</span><span class="sxs-lookup"><span data-stu-id="5a205-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="5a205-189">Dopo un periodo di raffreddamento di cinque minuti, se il numero medio di hello dei thread nelle macchine hello rimane 600, un altro computer viene aggiunto toohello set.</span><span class="sxs-lookup"><span data-stu-id="5a205-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="5a205-190">Se il numero di thread medio hello resta di sotto di 550, capacità hello del set di scalabilità hello viene ridotto di uno e un computer viene rimosso dal set di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="5a205-191">Impostare la scalabilità con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a205-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="5a205-192">esaminare toosee esempi dell'utilizzo di PowerShell tooset backup il ridimensionamento automatico [Azure monitoraggio PowerShell quick start esempi](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="5a205-193">Impostare la scalabilità con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5a205-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="5a205-194">esaminare toosee esempi dell'utilizzo di tooset CLI di Azure backup per la scalabilità automatica, [CLI multipiattaforma di Azure monitoraggio rapido avviare esempi](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="5a205-195">Impostare la scalabilità utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5a205-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="5a205-196">un esempio di utilizzo toosee hello tooset portale Azure backup per la scalabilità automatica, cercare in [creare un hello portale di Azure utilizzando Set di scalabilità macchina virtuale](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="5a205-197">Analisi delle azioni di ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="5a205-197">Investigate scaling actions</span></span>

* <span data-ttu-id="5a205-198">**Portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="5a205-198">**Azure portal**</span></span>  
<span data-ttu-id="5a205-199">Attualmente, è possibile ottenere una quantità limitata di informazioni tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="5a205-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="5a205-200">**Esplora risorse di Azure**</span><span class="sxs-lookup"><span data-stu-id="5a205-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="5a205-201">Questo strumento è hello migliore per l'esplorazione dello stato corrente di hello del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="5a205-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="5a205-202">Seguire questo percorso e dovrebbe essere vista istanza hello della scala hello imposta creato:</span><span class="sxs-lookup"><span data-stu-id="5a205-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="5a205-203">**Subscriptions > {sottoscrizione dell'utente} > resourceGroups > {gruppo di risorse dell'utente} > providers > Microsoft.Compute > virtualMachineScaleSets > {set di scalabilità dell'utente} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="5a205-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="5a205-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="5a205-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="5a205-205">Utilizzare questo comando tooget alcune informazioni:</span><span class="sxs-lookup"><span data-stu-id="5a205-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="5a205-206">Connessione macchina virtuale di toohello jumpbox esattamente come si farebbe qualsiasi altro computer e quindi è possibile accedere in remoto hello le macchine virtuali in hello scala set toomonitor singoli processi.</span><span class="sxs-lookup"><span data-stu-id="5a205-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a205-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a205-207">Next Steps</span></span>
* <span data-ttu-id="5a205-208">Esaminare [ridimensionare automaticamente le macchine in un Set di scalabilità della macchina virtuale](virtual-machine-scale-sets-windows-autoscale.md) toosee un esempio di come toocreate imposta una scala con il ridimensionamento automatico configurato.</span><span class="sxs-lookup"><span data-stu-id="5a205-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="5a205-209">Per alcuni esempi delle funzionalità di monitoraggio in Monitoraggio di Azure, vedere [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md) (Esempi di avvio rapido di PowerShell per Monitoraggio di Azure).</span><span class="sxs-lookup"><span data-stu-id="5a205-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="5a205-210">Informazioni sulle funzionalità di notifica di [utilizzare scalabilità automatica azioni toosend posta elettronica e ai webhook notifiche di avviso in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="5a205-211">Informazioni su come troppo[i log di controllo di utilizzare le notifiche degli avvisi di posta elettronica e ai webhook toosend in Monitoraggio di Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="5a205-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="5a205-212">Informazioni sugli [scenari di scalabilità automatica avanzata](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="5a205-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
