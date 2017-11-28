---
title: esempi di avvio rapido di aaaAzure PowerShell di monitoraggio. | Microsoft Docs
description: "Utilizzare PowerShell tooaccess funzionalità di monitoraggio di Azure quali scalabilità automatica, gli avvisi, webhook e la ricerca di log di attività."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="82b93-104">Esempi di avvio rapido con PowerShell per Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="82b93-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="82b93-105">In questo articolo viene indicato il campionamento toohelp di comandi di PowerShell accedere alle funzionalità di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="82b93-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="82b93-106">Monitoraggio di Azure consente tooAutoScale servizi Cloud, macchine virtuali e le applicazioni Web e toosend notifiche di avviso o URL web chiamata in base ai valori dei dati di telemetria configurato.</span><span class="sxs-lookup"><span data-stu-id="82b93-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="82b93-107">Monitoraggio di Azure è hello nuovo nome per ciò che è stato chiamato "Azure Insights" fino a 25 settembre 2016.</span><span class="sxs-lookup"><span data-stu-id="82b93-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="82b93-108">Tuttavia, gli spazi dei nomi hello e pertanto hello ancora i comandi seguenti contengono approfondite"hello".</span><span class="sxs-lookup"><span data-stu-id="82b93-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="82b93-109">Configurare PowerShell</span><span class="sxs-lookup"><span data-stu-id="82b93-109">Set up PowerShell</span></span>
<span data-ttu-id="82b93-110">Se hai già fatto, configurare toorun PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="82b93-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="82b93-111">Per ulteriori informazioni, vedere [come tooInstall e configurare PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82b93-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="82b93-112">Esempi in questo articolo</span><span class="sxs-lookup"><span data-stu-id="82b93-112">Examples in this article</span></span>
<span data-ttu-id="82b93-113">esempi di Hello di articolo hello illustrato come utilizzare i cmdlet di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="82b93-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="82b93-114">È inoltre possibile rivedere l'elenco completo di hello di cmdlet di PowerShell di monitoraggio di Azure in [i cmdlet di Azure Monitor (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b93-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="82b93-115">Eseguire l'acccesso e usare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="82b93-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="82b93-116">Innanzitutto, effettuare l'accesso tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="82b93-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="82b93-117">Questa operazione richiede toosign in.</span><span class="sxs-lookup"><span data-stu-id="82b93-117">This requires you toosign in.</span></span> <span data-ttu-id="82b93-118">Dopo aver effettuato l'accesso, vengono visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito.</span><span class="sxs-lookup"><span data-stu-id="82b93-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="82b93-119">Tutti hello lavoro cmdlet di Azure nel contesto di hello della sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="82b93-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="82b93-120">elenco di hello tooview delle sottoscrizioni si ha accesso a, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="82b93-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="82b93-121">toochange lavoro contesto tooa diversa sottoscrizione, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="82b93-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="82b93-122">Recuperare il registro attività per una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="82b93-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="82b93-123">Hello utilizzare `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82b93-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="82b93-124">Hello di seguito è riportati alcuni esempi comuni.</span><span class="sxs-lookup"><span data-stu-id="82b93-124">hello following are some common examples.</span></span>

<span data-ttu-id="82b93-125">Ottenere le voci di log da toopresent questa data e ora:</span><span class="sxs-lookup"><span data-stu-id="82b93-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="82b93-126">Ottenere le voci di log in un intervallo di date e ore:</span><span class="sxs-lookup"><span data-stu-id="82b93-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="82b93-127">Ottenere le voci di log da un gruppo di risorse specifico:</span><span class="sxs-lookup"><span data-stu-id="82b93-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="82b93-128">Ottenere le voci di log da un provider di risorse specifico in un intervallo di date e ore:</span><span class="sxs-lookup"><span data-stu-id="82b93-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="82b93-129">Ottenere tutte le voci di log con un chiamante specifico:</span><span class="sxs-lookup"><span data-stu-id="82b93-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="82b93-130">Hello comando Recupera hello ultimi 1.000 eventi dal log attività hello seguente:</span><span class="sxs-lookup"><span data-stu-id="82b93-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="82b93-131">`Get-AzureRmLog` supporta diversi altri parametri.</span><span class="sxs-lookup"><span data-stu-id="82b93-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="82b93-132">Vedere hello `Get-AzureRmLog` riferimento per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="82b93-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="82b93-133">`Get-AzureRmLog` fornisce solo 15 giorni di cronologia.</span><span class="sxs-lookup"><span data-stu-id="82b93-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="82b93-134">Utilizzo di hello **- MaxEvents** parametro consente tooquery hello ultimi N eventi, oltre a 15 giorni.</span><span class="sxs-lookup"><span data-stu-id="82b93-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="82b93-135">eventi tooaccess anteriori a 15 giorni, utilizzare hello API REST o SDK (esempio di c# utilizzando hello SDK).</span><span class="sxs-lookup"><span data-stu-id="82b93-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="82b93-136">Se non si include **StartTime**, il valore predefinito di hello **EndTime** meno di un'ora.</span><span class="sxs-lookup"><span data-stu-id="82b93-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="82b93-137">Se non si include **EndTime**, il valore predefinito di hello ora corrente.</span><span class="sxs-lookup"><span data-stu-id="82b93-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="82b93-138">Tutte le ore sono in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="82b93-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="82b93-139">Recupero della cronologia di avvisi</span><span class="sxs-lookup"><span data-stu-id="82b93-139">Retrieve alerts history</span></span>
<span data-ttu-id="82b93-140">tutti gli eventi di allarme, è possibile eseguire query tooview hello registri di gestione risorse di Azure mediante hello seguono esempi.</span><span class="sxs-lookup"><span data-stu-id="82b93-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="82b93-141">regola di cronologia di hello tooview per un avviso specifico, è possibile utilizzare hello `Get-AzureRmAlertHistory` cmdlet, il passaggio di ID di risorsa hello della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="82b93-142">Hello `Get-AzureRmAlertHistory` cmdlet supporta vari parametri.</span><span class="sxs-lookup"><span data-stu-id="82b93-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="82b93-143">Per altre informazioni, vedere [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b93-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="82b93-144">Recupero delle informazioni sulle regole di avviso</span><span class="sxs-lookup"><span data-stu-id="82b93-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="82b93-145">Tutti i seguenti comandi hello agiscono su un gruppo di risorse denominato "montest".</span><span class="sxs-lookup"><span data-stu-id="82b93-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="82b93-146">Visualizzare tutte le proprietà di hello della regola di avviso hello:</span><span class="sxs-lookup"><span data-stu-id="82b93-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="82b93-147">Recuperare tutti gli avvisi in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="82b93-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="82b93-148">Recuperare tutte le regole di avviso impostate per una risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="82b93-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="82b93-149">Ad esempio, tutte le regole di avviso impostate su una VM.</span><span class="sxs-lookup"><span data-stu-id="82b93-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="82b93-150">`Get-AzureRmAlertRule` supporta altri parametri.</span><span class="sxs-lookup"><span data-stu-id="82b93-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="82b93-151">Per altre informazioni, vedere [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) .</span><span class="sxs-lookup"><span data-stu-id="82b93-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="82b93-152">Creare avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="82b93-152">Create metric alerts</span></span>
<span data-ttu-id="82b93-153">È possibile utilizzare hello `Add-AlertRule` toocreate cmdlet, aggiornare o disabilitare una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="82b93-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="82b93-154">È possibile creare proprietà di posta elettronica e webhook usando rispettivamente `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`.</span><span class="sxs-lookup"><span data-stu-id="82b93-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="82b93-155">Nel cmdlet hello regola di avviso per assegnare queste come azioni toohello **azioni** proprietà della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="82b93-156">Hello nella tabella seguente vengono descritti i parametri di hello e valori utilizzati toocreate un avviso utilizzando una metrica.</span><span class="sxs-lookup"><span data-stu-id="82b93-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="82b93-157">parametro</span><span class="sxs-lookup"><span data-stu-id="82b93-157">parameter</span></span> | <span data-ttu-id="82b93-158">value</span><span class="sxs-lookup"><span data-stu-id="82b93-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="82b93-159">Nome</span><span class="sxs-lookup"><span data-stu-id="82b93-159">Name</span></span> |<span data-ttu-id="82b93-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="82b93-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="82b93-161">Posizione di questa regola di avviso</span><span class="sxs-lookup"><span data-stu-id="82b93-161">Location of this alert rule</span></span> |<span data-ttu-id="82b93-162">Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="82b93-162">East US</span></span> |
| <span data-ttu-id="82b93-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82b93-163">ResourceGroup</span></span> |<span data-ttu-id="82b93-164">montest</span><span class="sxs-lookup"><span data-stu-id="82b93-164">montest</span></span> |
| <span data-ttu-id="82b93-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="82b93-165">TargetResourceId</span></span> |<span data-ttu-id="82b93-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="82b93-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="82b93-167">MetricName di avviso hello creato</span><span class="sxs-lookup"><span data-stu-id="82b93-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="82b93-168">\PhysicalDisk ( totale) \Disk scritture al secondo. Vedere hello `Get-MetricDefinitions` come tooretrieve hello esatti nomi di metrica relativi ai cmdlet di</span><span class="sxs-lookup"><span data-stu-id="82b93-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="82b93-169">operator</span><span class="sxs-lookup"><span data-stu-id="82b93-169">operator</span></span> |<span data-ttu-id="82b93-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="82b93-170">GreaterThan</span></span> |
| <span data-ttu-id="82b93-171">Valore soglia (conteggio al secondo per questa metrica)</span><span class="sxs-lookup"><span data-stu-id="82b93-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="82b93-172">1</span><span class="sxs-lookup"><span data-stu-id="82b93-172">1</span></span> |
| <span data-ttu-id="82b93-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="82b93-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="82b93-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="82b93-174">00:05:00</span></span> |
| <span data-ttu-id="82b93-175">Aggregator (statistica della metrica di hello, che utilizza il numero medio, in questo caso)</span><span class="sxs-lookup"><span data-stu-id="82b93-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="82b93-176">Media</span><span class="sxs-lookup"><span data-stu-id="82b93-176">Average</span></span> |
| <span data-ttu-id="82b93-177">indirizzi di posta elettronica personalizzati (matrice di stringhe)</span><span class="sxs-lookup"><span data-stu-id="82b93-177">custom emails (string array)</span></span> |<span data-ttu-id="82b93-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="82b93-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="82b93-179">Invia messaggio di posta elettronica tooowners, contributors e readers</span><span class="sxs-lookup"><span data-stu-id="82b93-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="82b93-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="82b93-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="82b93-181">Creare un'azione Email</span><span class="sxs-lookup"><span data-stu-id="82b93-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="82b93-182">Creazione di un’azione Webhook</span><span class="sxs-lookup"><span data-stu-id="82b93-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="82b93-183">Crea regola di avviso hello nella metrica % della CPU di hello in una VM classica</span><span class="sxs-lookup"><span data-stu-id="82b93-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="82b93-184">Recuperare la regola di avviso hello</span><span class="sxs-lookup"><span data-stu-id="82b93-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="82b93-185">Hello Aggiungi avviso cmdlet Aggiorna regola hello anche se per hello proprietà specificato esiste già una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="82b93-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="82b93-186">toodisable una regola di avviso, includere il parametro hello **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="82b93-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="82b93-187">Acquisizione di un elenco delle metriche disponibili per gli avvisi</span><span class="sxs-lookup"><span data-stu-id="82b93-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="82b93-188">È possibile utilizzare hello `Get-AzureRmMetricDefinition` cmdlet tooview hello elenco tutte le metriche per una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="82b93-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="82b93-189">Hello esempio seguente genera una tabella con nome metrica di hello e hello unità per tale.</span><span class="sxs-lookup"><span data-stu-id="82b93-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="82b93-190">Un elenco completo delle opzioni disponibili per `Get-AzureRmMetricDefinition` si trova in [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b93-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="82b93-191">Creazione e gestione delle impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="82b93-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="82b93-192">Una risorsa, ad esempio un'app Web, una macchina virtuale, un servizio cloud o un set di scalabilità di macchine virtuali, può avere una sola impostazione di scalabilità automatica configurata.</span><span class="sxs-lookup"><span data-stu-id="82b93-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="82b93-193">Tuttavia, ogni impostazione di scalabilità automatica può includere diversi profili.</span><span class="sxs-lookup"><span data-stu-id="82b93-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="82b93-194">Ad esempio, un profilo di scalabilità in base alle prestazioni e un altro profilo basato sulla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="82b93-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="82b93-195">Ogni profilo può avere più regole associate configurate.</span><span class="sxs-lookup"><span data-stu-id="82b93-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="82b93-196">Per ulteriori informazioni sulla scalabilità automatica, vedere [come un'applicazione tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="82b93-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="82b93-197">Ecco i passaggi di hello che verrà utilizzato:</span><span class="sxs-lookup"><span data-stu-id="82b93-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="82b93-198">Creare le regole.</span><span class="sxs-lookup"><span data-stu-id="82b93-198">Create rule(s).</span></span>
2. <span data-ttu-id="82b93-199">Creare profili hello mapping regole creata in precedenza toohello profili.</span><span class="sxs-lookup"><span data-stu-id="82b93-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="82b93-200">Facoltativo: creare notifiche per la scalabilità automatica configurando le proprietà di webhook e posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="82b93-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="82b93-201">Creare un'impostazione di scalabilità automatica con un nome sulla risorsa di destinazione hello eseguendo il mapping di profili di hello e notifiche creato nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="82b93-202">Hello esempi seguenti si illustra come creare un'impostazione di scalabilità automatica per un Set di scalabilità macchina virtuale per un sistema operativo Windows basato mediante la metrica di utilizzo della CPU hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="82b93-203">Innanzitutto, creare una regola tooscale in orizzontale, con un aumento del numero di istanza.</span><span class="sxs-lookup"><span data-stu-id="82b93-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="82b93-204">Successivamente, creare una regola tooscale, con una riduzione del numero di istanza.</span><span class="sxs-lookup"><span data-stu-id="82b93-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="82b93-205">Quindi, creare un profilo per le regole di hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="82b93-206">Creare una proprietà webhook.</span><span class="sxs-lookup"><span data-stu-id="82b93-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="82b93-207">Creare la proprietà di notifica di hello per l'impostazione di scalabilità automatica hello, inclusa la posta elettronica e hello webhook creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82b93-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="82b93-208">Creare infine hello scalabilità automatica impostazione tooadd hello profilo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="82b93-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="82b93-209">Per altre informazioni sulla gestione delle impostazioni di scalabilità automatica, vedere [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b93-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="82b93-210">Cronologia di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="82b93-210">Autoscale history</span></span>
<span data-ttu-id="82b93-211">Hello seguente esempio viene illustrato come visualizzare gli eventi di ridimensionamento automatico e avviso recente.</span><span class="sxs-lookup"><span data-stu-id="82b93-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="82b93-212">Utilizzare hello attività tooview hello scalabilità automatica cronologia di ricerca.</span><span class="sxs-lookup"><span data-stu-id="82b93-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="82b93-213">È possibile utilizzare hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve cronologia scalabilità.</span><span class="sxs-lookup"><span data-stu-id="82b93-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="82b93-214">Per altre informazioni, vedere [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b93-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="82b93-215">Visualizzazione dei dettagli per un'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="82b93-215">View details for an autoscale setting</span></span>
<span data-ttu-id="82b93-216">È possibile utilizzare hello `Get-Autoscalesetting` cmdlet tooretrieve ulteriori informazioni sull'impostazione di scalabilità automatica hello.</span><span class="sxs-lookup"><span data-stu-id="82b93-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="82b93-217">Hello esempio seguente mostra informazioni dettagliate su tutte le impostazioni di scalabilità automatica nel gruppo di risorse hello 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="82b93-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="82b93-218">Hello esempio seguente mostra i dettagli di tutte le impostazioni di scalabilità automatica nel gruppo di risorse hello 'myrg1' e in particolare hello denominato 'MyScaleVMSSSetting' impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="82b93-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="82b93-219">Rimozione di un'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="82b93-219">Remove an autoscale setting</span></span>
<span data-ttu-id="82b93-220">È possibile utilizzare hello `Remove-Autoscalesetting` cmdlet toodelete un'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="82b93-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="82b93-221">Gestione dei profili di log per i registri attività</span><span class="sxs-lookup"><span data-stu-id="82b93-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="82b93-222">È possibile creare un *log profilo* e l'esportazione dei dati da account di archiviazione tooa log attività ed è possibile configurare conservazione dei dati per tale.</span><span class="sxs-lookup"><span data-stu-id="82b93-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="82b93-223">Facoltativamente, è inoltre possibile trasmettere hello dati tooyour Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="82b93-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="82b93-224">Questa funzionalità attualmente è in anteprima ed è possibile creare solo un profilo di log per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="82b93-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="82b93-225">È possibile utilizzare hello seguente cmdlet con il toocreate sottoscrizione corrente e gestire i profili di log.</span><span class="sxs-lookup"><span data-stu-id="82b93-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="82b93-226">È anche possibile scegliere una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="82b93-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="82b93-227">Anche se la sottoscrizione corrente toohello impostazioni predefinite di PowerShell è sempre possibile modificare tale tramite `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="82b93-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="82b93-228">È possibile configurare l'account di archiviazione tooany dati tooroute log attività o l'Hub di eventi all'interno di tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="82b93-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="82b93-229">I dati sono scritti come file di BLOB in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="82b93-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="82b93-230">Acquisizione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="82b93-230">Get a log profile</span></span>
<span data-ttu-id="82b93-231">toofetch i profili di log esistente, utilizzare hello `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82b93-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="82b93-232">Aggiunta di un profilo di log senza conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="82b93-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="82b93-233">Rimozione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="82b93-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="82b93-234">Aggiunta di un profilo di log con conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="82b93-234">Add a log profile with data retention</span></span>
<span data-ttu-id="82b93-235">È possibile specificare hello **- RetentionInDays** proprietà con hello numero di giorni, come un numero intero positivo, in cui i dati di hello verranno mantenuti.</span><span class="sxs-lookup"><span data-stu-id="82b93-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="82b93-236">Aggiunta di un profilo di log con conservazione e hub di eventi</span><span class="sxs-lookup"><span data-stu-id="82b93-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="82b93-237">In aggiunta toorouting account toostorage di dati, è possibile anche trasmetterlo tramite flusso tooan Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="82b93-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="82b93-238">Si noti che in questa versione di anteprima release e hello configurazione di account di archiviazione è obbligatorio ma configurazione Hub eventi è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="82b93-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="82b93-239">Configurazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="82b93-239">Configure diagnostics logs</span></span>
<span data-ttu-id="82b93-240">Molti servizi di Azure forniscono i log e dati di telemetria che possono essere dati toosave configurata nell'account di archiviazione di Azure, inviare tooEvent hub e/o inviati tooan dell'area di lavoro OMS Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="82b93-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="82b93-241">Tale operazione può essere eseguita solo a un livello di risorse e hub di eventi o di account di archiviazione hello devono essere presenti in hello stessa area risorse di destinazione hello in hello diagnostica è configurata.</span><span class="sxs-lookup"><span data-stu-id="82b93-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="82b93-242">Acquisizione dell’impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="82b93-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="82b93-243">Disabilitazione dell’impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="82b93-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="82b93-244">Abilitazione dell'impostazione di diagnostica senza conservazione</span><span class="sxs-lookup"><span data-stu-id="82b93-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="82b93-245">Abilitazione dell'impostazione di diagnostica con conservazione</span><span class="sxs-lookup"><span data-stu-id="82b93-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="82b93-246">Abilitazione dell’impostazione di diagnostica con conservazione per una categoria di log specifica</span><span class="sxs-lookup"><span data-stu-id="82b93-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="82b93-247">Abilitazione dell'impostazione di diagnostica per hub eventi</span><span class="sxs-lookup"><span data-stu-id="82b93-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="82b93-248">Abilitazione dell'impostazione di diagnostica per OMS</span><span class="sxs-lookup"><span data-stu-id="82b93-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
