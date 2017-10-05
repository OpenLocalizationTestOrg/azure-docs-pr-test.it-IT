---
title: Esempi di avvio rapido con PowerShell per Monitoraggio di Azure. | Microsoft Docs
description: "Usare PowerShell per accedere alle funzionalità di Monitoraggio di Azure, ad esempio scalabilità automatica, avvisi, webhook e ricerca nei log attività."
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
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="c79eb-104">Esempi di avvio rapido con PowerShell per Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="c79eb-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="c79eb-105">Questo articolo illustra comandi di PowerShell di esempio per accedere rapidamente alle funzionalità di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="c79eb-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="c79eb-106">Monitoraggio di Azure consente di ridimensionare automaticamente servizi cloud, macchine virtuali e app Web e di inviare notifiche di avviso o chiamare URL Web in base ai valori dei dati di telemetria configurati.</span><span class="sxs-lookup"><span data-stu-id="c79eb-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="c79eb-107">Dal 25 settembre 2016 Monitoraggio di Azure è il nuovo nome di "Azure Insights".</span><span class="sxs-lookup"><span data-stu-id="c79eb-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="c79eb-108">Tuttavia, gli spazi dei nomi e quindi i comandi seguenti contengono ancora il termine "insights".</span><span class="sxs-lookup"><span data-stu-id="c79eb-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="c79eb-109">Configurare PowerShell</span><span class="sxs-lookup"><span data-stu-id="c79eb-109">Set up PowerShell</span></span>
<span data-ttu-id="c79eb-110">Se non è ancora stato fatto, configurare PowerShell per l'esecuzione sul computer.</span><span class="sxs-lookup"><span data-stu-id="c79eb-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="c79eb-111">Per altre informazioni, vedere [Come installare e configurare PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c79eb-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="c79eb-112">Esempi in questo articolo</span><span class="sxs-lookup"><span data-stu-id="c79eb-112">Examples in this article</span></span>
<span data-ttu-id="c79eb-113">Gli esempi in questo articolo illustrano come usare i cmdlet di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="c79eb-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="c79eb-114">È anche possibile esaminare l'elenco completo di cmdlet di PowerShell di Monitoraggio di Azure nell'argomento relativo ai [cmdlet di Monitoraggio di Azure(Azure Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79eb-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="c79eb-115">Eseguire l'acccesso e usare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="c79eb-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="c79eb-116">Per prima cosa, accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c79eb-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="c79eb-117">Questo richiede di effettuare l’accesso.</span><span class="sxs-lookup"><span data-stu-id="c79eb-117">This requires you to sign in.</span></span> <span data-ttu-id="c79eb-118">Dopo aver effettuato l'accesso, vengono visualizzati l'account, l'ID tenant e l'ID sottoscrizione predefinito.</span><span class="sxs-lookup"><span data-stu-id="c79eb-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="c79eb-119">Tutti i cmdlet di Azure funzionano nel contesto della sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c79eb-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="c79eb-120">Per visualizzare l'elenco delle sottoscrizioni accessibili, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c79eb-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="c79eb-121">Per modificare il contesto di lavoro in una sottoscrizione diversa, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c79eb-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="c79eb-122">Recuperare il registro attività per una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="c79eb-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="c79eb-123">Utilizzare il cmdlet `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="c79eb-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="c79eb-124">Di seguito sono riportati alcuni esempi comuni.</span><span class="sxs-lookup"><span data-stu-id="c79eb-124">The following are some common examples.</span></span>

<span data-ttu-id="c79eb-125">Ottenere le voci di log da questa data e ora fino a oggi:</span><span class="sxs-lookup"><span data-stu-id="c79eb-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="c79eb-126">Ottenere le voci di log in un intervallo di date e ore:</span><span class="sxs-lookup"><span data-stu-id="c79eb-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c79eb-127">Ottenere le voci di log da un gruppo di risorse specifico:</span><span class="sxs-lookup"><span data-stu-id="c79eb-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="c79eb-128">Ottenere le voci di log da un provider di risorse specifico in un intervallo di date e ore:</span><span class="sxs-lookup"><span data-stu-id="c79eb-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="c79eb-129">Ottenere tutte le voci di log con un chiamante specifico:</span><span class="sxs-lookup"><span data-stu-id="c79eb-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="c79eb-130">Il comando seguente recupera gli ultimi 1000 eventi dal registro attività:</span><span class="sxs-lookup"><span data-stu-id="c79eb-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="c79eb-131">`Get-AzureRmLog` supporta diversi altri parametri.</span><span class="sxs-lookup"><span data-stu-id="c79eb-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="c79eb-132">Per altre informazioni, vedere il riferimento `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="c79eb-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="c79eb-133">`Get-AzureRmLog` fornisce solo 15 giorni di cronologia.</span><span class="sxs-lookup"><span data-stu-id="c79eb-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="c79eb-134">L’uso del parametro **-MaxEvents** consente di eseguire una query sugli ultimi N eventi, oltre i 15 giorni.</span><span class="sxs-lookup"><span data-stu-id="c79eb-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="c79eb-135">Per accedere agli eventi precedenti ai 15 giorni, usare l'API REST o l'SDK (esempio di C# tramite il SDK).</span><span class="sxs-lookup"><span data-stu-id="c79eb-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="c79eb-136">Se non si include **StartTime**, il valore predefinito è **EndTime** meno un'ora.</span><span class="sxs-lookup"><span data-stu-id="c79eb-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="c79eb-137">Se non si include **EndTime**, il valore predefinito è l’ora corrente.</span><span class="sxs-lookup"><span data-stu-id="c79eb-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="c79eb-138">Tutte le ore sono in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="c79eb-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="c79eb-139">Recupero della cronologia di avvisi</span><span class="sxs-lookup"><span data-stu-id="c79eb-139">Retrieve alerts history</span></span>
<span data-ttu-id="c79eb-140">Per visualizzare tutti gli eventi di avviso, è possibile eseguire query in Azure Resource Manager usando gli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c79eb-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c79eb-141">Per visualizzare la cronologia per una regola avviso specifica, è possibile utilizzare il cmdlet `Get-AzureRmAlertHistory` passando l'ID risorsa della regola avvisi.</span><span class="sxs-lookup"><span data-stu-id="c79eb-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="c79eb-142">Il cmdlet `Get-AzureRmAlertHistory` supporta diversi parametri.</span><span class="sxs-lookup"><span data-stu-id="c79eb-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="c79eb-143">Per altre informazioni, vedere [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79eb-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="c79eb-144">Recupero delle informazioni sulle regole di avviso</span><span class="sxs-lookup"><span data-stu-id="c79eb-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="c79eb-145">Tutti i comandi seguenti agiscono su un gruppo di risorse chiamato "montest".</span><span class="sxs-lookup"><span data-stu-id="c79eb-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="c79eb-146">Visualizzare tutte le proprietà della regola di avviso:</span><span class="sxs-lookup"><span data-stu-id="c79eb-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="c79eb-147">Recuperare tutti gli avvisi in un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="c79eb-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="c79eb-148">Recuperare tutte le regole di avviso impostate per una risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c79eb-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="c79eb-149">Ad esempio, tutte le regole di avviso impostate su una VM.</span><span class="sxs-lookup"><span data-stu-id="c79eb-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="c79eb-150">`Get-AzureRmAlertRule` supporta altri parametri.</span><span class="sxs-lookup"><span data-stu-id="c79eb-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="c79eb-151">Per altre informazioni, vedere [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c79eb-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="c79eb-152">Creare avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="c79eb-152">Create metric alerts</span></span>
<span data-ttu-id="c79eb-153">È possibile utilizzare il cmdlet `Add-AlertRule` per creare, aggiornare o disabilitare una regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="c79eb-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="c79eb-154">È possibile creare proprietà di posta elettronica e webhook usando rispettivamente `New-AzureRmAlertRuleEmail` e `New-AzureRmAlertRuleWebhook`.</span><span class="sxs-lookup"><span data-stu-id="c79eb-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="c79eb-155">Nel cmdlet per la regola avvisi assegnare queste azioni alla proprietà **Actions** della regola avvisi.</span><span class="sxs-lookup"><span data-stu-id="c79eb-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="c79eb-156">La tabella seguente descrive i parametri e valori usati per creare un avviso tramite una metrica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="c79eb-157">parametro</span><span class="sxs-lookup"><span data-stu-id="c79eb-157">parameter</span></span> | <span data-ttu-id="c79eb-158">value</span><span class="sxs-lookup"><span data-stu-id="c79eb-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="c79eb-159">Nome</span><span class="sxs-lookup"><span data-stu-id="c79eb-159">Name</span></span> |<span data-ttu-id="c79eb-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="c79eb-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="c79eb-161">Posizione di questa regola di avviso</span><span class="sxs-lookup"><span data-stu-id="c79eb-161">Location of this alert rule</span></span> |<span data-ttu-id="c79eb-162">Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="c79eb-162">East US</span></span> |
| <span data-ttu-id="c79eb-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c79eb-163">ResourceGroup</span></span> |<span data-ttu-id="c79eb-164">montest</span><span class="sxs-lookup"><span data-stu-id="c79eb-164">montest</span></span> |
| <span data-ttu-id="c79eb-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="c79eb-165">TargetResourceId</span></span> |<span data-ttu-id="c79eb-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="c79eb-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="c79eb-167">MetricName dell'avviso creato</span><span class="sxs-lookup"><span data-stu-id="c79eb-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="c79eb-168">\PhysicalDisk ( totale) \Disk scritture al secondo. Vedere il `Get-MetricDefinitions` cmdlet su come recuperare i nomi di metrica esatti</span><span class="sxs-lookup"><span data-stu-id="c79eb-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="c79eb-169">operator</span><span class="sxs-lookup"><span data-stu-id="c79eb-169">operator</span></span> |<span data-ttu-id="c79eb-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="c79eb-170">GreaterThan</span></span> |
| <span data-ttu-id="c79eb-171">Valore soglia (conteggio al secondo per questa metrica)</span><span class="sxs-lookup"><span data-stu-id="c79eb-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="c79eb-172">1</span><span class="sxs-lookup"><span data-stu-id="c79eb-172">1</span></span> |
| <span data-ttu-id="c79eb-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="c79eb-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="c79eb-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="c79eb-174">00:05:00</span></span> |
| <span data-ttu-id="c79eb-175">aggregatore (statistica della metrica che usa il numero medio, in questo caso)</span><span class="sxs-lookup"><span data-stu-id="c79eb-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="c79eb-176">Media</span><span class="sxs-lookup"><span data-stu-id="c79eb-176">Average</span></span> |
| <span data-ttu-id="c79eb-177">indirizzi di posta elettronica personalizzati (matrice di stringhe)</span><span class="sxs-lookup"><span data-stu-id="c79eb-177">custom emails (string array)</span></span> |<span data-ttu-id="c79eb-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="c79eb-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="c79eb-179">invio di messaggi di posta elettronica a proprietari, collaboratori e lettori</span><span class="sxs-lookup"><span data-stu-id="c79eb-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="c79eb-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="c79eb-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="c79eb-181">Creare un'azione Email</span><span class="sxs-lookup"><span data-stu-id="c79eb-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="c79eb-182">Creazione di un’azione Webhook</span><span class="sxs-lookup"><span data-stu-id="c79eb-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="c79eb-183">Creazione di una regola di avviso sulla metrica CPU% per una VM classica</span><span class="sxs-lookup"><span data-stu-id="c79eb-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="c79eb-184">Recupero di una regola di avviso</span><span class="sxs-lookup"><span data-stu-id="c79eb-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c79eb-185">Il cmdlet Aggiungi avviso aggiorna anche la regola se esiste già una regola di avviso per le proprietà specificate.</span><span class="sxs-lookup"><span data-stu-id="c79eb-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="c79eb-186">Per disabilitare una regola di avviso, includere il parametro **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="c79eb-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="c79eb-187">Acquisizione di un elenco delle metriche disponibili per gli avvisi</span><span class="sxs-lookup"><span data-stu-id="c79eb-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="c79eb-188">Usare il cmdlet `Get-AzureRmMetricDefinition` per visualizzare l'elenco di tutte le metriche per una specifica risorsa.</span><span class="sxs-lookup"><span data-stu-id="c79eb-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="c79eb-189">L'esempio seguente genera una tabella con la metrica Name e il  relativo valore Unit.</span><span class="sxs-lookup"><span data-stu-id="c79eb-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="c79eb-190">Un elenco completo delle opzioni disponibili per `Get-AzureRmMetricDefinition` si trova in [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79eb-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="c79eb-191">Creazione e gestione delle impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="c79eb-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="c79eb-192">Una risorsa, ad esempio un'app Web, una macchina virtuale, un servizio cloud o un set di scalabilità di macchine virtuali, può avere una sola impostazione di scalabilità automatica configurata.</span><span class="sxs-lookup"><span data-stu-id="c79eb-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="c79eb-193">Tuttavia, ogni impostazione di scalabilità automatica può includere diversi profili.</span><span class="sxs-lookup"><span data-stu-id="c79eb-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="c79eb-194">Ad esempio, un profilo di scalabilità in base alle prestazioni e un altro profilo basato sulla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="c79eb-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="c79eb-195">Ogni profilo può avere più regole associate configurate.</span><span class="sxs-lookup"><span data-stu-id="c79eb-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="c79eb-196">Per altre informazioni sulla scalabilità automatica, vedere [Come configurare la scalabilità automatica di un servizio cloud](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c79eb-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="c79eb-197">Ecco i passaggi da utilizzare:</span><span class="sxs-lookup"><span data-stu-id="c79eb-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="c79eb-198">Creare le regole.</span><span class="sxs-lookup"><span data-stu-id="c79eb-198">Create rule(s).</span></span>
2. <span data-ttu-id="c79eb-199">Creare i profili eseguendo il mapping delle regole create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c79eb-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="c79eb-200">Facoltativo: creare notifiche per la scalabilità automatica configurando le proprietà di webhook e posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="c79eb-201">Creare un'impostazione di scalabilità automatica con un nome per la risorsa di destinazione associando profili e notifiche creati nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c79eb-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="c79eb-202">Gli esempi seguenti illustrano come creare un'impostazione di scalabilità automatica per un set di scalabilità di macchine virtuali per un sistema operativo Windows in base alla metrica di utilizzo della CPU.</span><span class="sxs-lookup"><span data-stu-id="c79eb-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="c79eb-203">Per prima cosa, creare una regola per aumentare il numero di istanze, con un incremento del numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="c79eb-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="c79eb-204">Creare poi una regola per ridurre il numero di istanze, con una diminuzione di una istanza.</span><span class="sxs-lookup"><span data-stu-id="c79eb-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="c79eb-205">A questo punto, creare un profilo per le regole.</span><span class="sxs-lookup"><span data-stu-id="c79eb-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="c79eb-206">Creare una proprietà webhook.</span><span class="sxs-lookup"><span data-stu-id="c79eb-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="c79eb-207">Creare la proprietà di notifica per l'impostazione di scalabilità automatica, tra cui posta elettronica e webhook create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c79eb-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="c79eb-208">Infine, creare l'impostazione di scalabilità automatica da aggiungere al profilo appena creato.</span><span class="sxs-lookup"><span data-stu-id="c79eb-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="c79eb-209">Per altre informazioni sulla gestione delle impostazioni di scalabilità automatica, vedere [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79eb-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="c79eb-210">Cronologia di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="c79eb-210">Autoscale history</span></span>
<span data-ttu-id="c79eb-211">Il seguente esempio illustra come visualizzare gli eventi di scalabilità automatica e avviso recenti.</span><span class="sxs-lookup"><span data-stu-id="c79eb-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="c79eb-212">Usare la ricerca dei registri attività per consultare la cronologia di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="c79eb-213">È possibile usare il cmdlet `Get-AzureRmAutoScaleHistory` per recuperare la cronologia di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="c79eb-214">Per altre informazioni, vedere [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="c79eb-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="c79eb-215">Visualizzazione dei dettagli per un'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="c79eb-215">View details for an autoscale setting</span></span>
<span data-ttu-id="c79eb-216">È possibile usare il cmdlet `Get-Autoscalesetting` per recuperare altre informazioni sull'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="c79eb-217">L'esempio seguente mostra dettagli su tutte le impostazioni di scalabilità automatica nel gruppo di risorse 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="c79eb-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="c79eb-218">L'esempio seguente mostra i dettagli su tutte le impostazioni di scalabilità automatica nel gruppo di risorse 'myrg1' e in particolare l'impostazione di scalabilità automatica denominata 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="c79eb-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="c79eb-219">Rimozione di un'impostazione di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="c79eb-219">Remove an autoscale setting</span></span>
<span data-ttu-id="c79eb-220">È possibile usare il cmdlet `Remove-Autoscalesetting` per eliminare un'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="c79eb-221">Gestione dei profili di log per i registri attività</span><span class="sxs-lookup"><span data-stu-id="c79eb-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="c79eb-222">È possibile creare un *profilo di log* ed esportare i dati dai registri attività in un account di archiviazione ed è possibile configurare la relativa conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c79eb-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="c79eb-223">Facoltativamente, è inoltre possibile trasmettere i dati all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c79eb-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="c79eb-224">Questa funzionalità attualmente è in anteprima ed è possibile creare solo un profilo di log per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c79eb-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="c79eb-225">Per creare e gestire i profili di log, è possibile usare i cmdlet seguenti con la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="c79eb-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="c79eb-226">È anche possibile scegliere una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="c79eb-227">Anche se PowerShell usa la sottoscrizione corrente per impostazione predefinita, è sempre possibile modificarla usando `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="c79eb-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="c79eb-228">È possibile configurare i registri attività per indirizzare i dati a qualsiasi account di archiviazione o all'hub eventi all'interno di tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c79eb-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="c79eb-229">I dati sono scritti come file di BLOB in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c79eb-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="c79eb-230">Acquisizione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="c79eb-230">Get a log profile</span></span>
<span data-ttu-id="c79eb-231">Per recuperare i profili di log esistenti, usare il cmdlet `Get-AzureRmLogProfile` .</span><span class="sxs-lookup"><span data-stu-id="c79eb-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="c79eb-232">Aggiunta di un profilo di log senza conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="c79eb-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="c79eb-233">Rimozione di un profilo di log</span><span class="sxs-lookup"><span data-stu-id="c79eb-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="c79eb-234">Aggiunta di un profilo di log con conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="c79eb-234">Add a log profile with data retention</span></span>
<span data-ttu-id="c79eb-235">È possibile specificare la proprietà **-RetentionInDays** con il numero di giorni, sotto forma di numero intero positivo, per i quali i dati vengono conservati.</span><span class="sxs-lookup"><span data-stu-id="c79eb-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="c79eb-236">Aggiunta di un profilo di log con conservazione e hub di eventi</span><span class="sxs-lookup"><span data-stu-id="c79eb-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="c79eb-237">Oltre a instradare i dati a un account di archiviazione, è anche possibile trasmetterli all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c79eb-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="c79eb-238">In questa versione di anteprima, la configurazione dell'account di archiviazione è obbligatoria, mentre quella dell’hub di eventi è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c79eb-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="c79eb-239">Configurazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="c79eb-239">Configure diagnostics logs</span></span>
<span data-ttu-id="c79eb-240">Molti servizi di Azure fornisce log e dati di telemetria aggiuntivi che possono essere configurati per salvare i dati nell'account di Archiviazione di Azure, inviare dati all'hub eventi e/o inviare dati a un'area di lavoro di Log Analytics di OMS.</span><span class="sxs-lookup"><span data-stu-id="c79eb-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="c79eb-241">Tale operazione può essere eseguita solo a livello di risorse e l'account di archiviazione o l'hub eventi deve essere presente nella stessa area come risorsa di destinazione in cui viene configurata l'impostazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="c79eb-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="c79eb-242">Acquisizione dell’impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="c79eb-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="c79eb-243">Disabilitazione dell’impostazione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="c79eb-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="c79eb-244">Abilitazione dell'impostazione di diagnostica senza conservazione</span><span class="sxs-lookup"><span data-stu-id="c79eb-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="c79eb-245">Abilitazione dell'impostazione di diagnostica con conservazione</span><span class="sxs-lookup"><span data-stu-id="c79eb-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c79eb-246">Abilitazione dell’impostazione di diagnostica con conservazione per una categoria di log specifica</span><span class="sxs-lookup"><span data-stu-id="c79eb-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="c79eb-247">Abilitazione dell'impostazione di diagnostica per hub eventi</span><span class="sxs-lookup"><span data-stu-id="c79eb-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="c79eb-248">Abilitazione dell'impostazione di diagnostica per OMS</span><span class="sxs-lookup"><span data-stu-id="c79eb-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
