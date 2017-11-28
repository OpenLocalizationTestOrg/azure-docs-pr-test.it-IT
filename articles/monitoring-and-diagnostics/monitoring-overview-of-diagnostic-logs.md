---
title: aaaOverview dei log di diagnostica di Azure | Documenti Microsoft
description: "Informazioni su quali sono i log di diagnostica Azure e come è possibile usarli toounderstand eventi che si verificano all'interno di una risorsa di Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="9878e-103">Raccogliere e usare i dati dei log dalle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="9878e-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="9878e-104">Definizione di log di diagnostica di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="9878e-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="9878e-105">**I log di diagnostica a livello di risorse Azure** sono registri generati da una risorsa che forniscono dati completo e frequenti sull'operazione di hello di tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="9878e-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="9878e-106">contenuto Hello di questi log varia in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="9878e-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="9878e-107">I contatori delle regole di gruppo di sicurezza di rete e i controlli di insieme di credenziali delle chiavi, ad esempio, sono due categorie di log di risorsa.</span><span class="sxs-lookup"><span data-stu-id="9878e-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="9878e-108">I log di diagnostica a livello di risorse diversi da hello [Log attività](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9878e-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="9878e-109">Log attività Hello fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione tramite Gestione risorse, ad esempio, la creazione di una macchina virtuale o l'eliminazione di un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="9878e-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="9878e-110">Log attività Hello è un log a livello di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9878e-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="9878e-111">I log di diagnostica a livello di risorsa includono informazioni sulle operazioni eseguite all'interno della risorsa stessa, ad esempio, il recupero di un segreto da un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="9878e-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="9878e-112">I log di diagnostica a livello di risorsa differiscono anche dal log di diagnostica a livello del sistema operativo guest.</span><span class="sxs-lookup"><span data-stu-id="9878e-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="9878e-113">I log di diagnostica del sistema operativo guest vengono compilati da un agente in esecuzione all'interno di una macchina virtuale o di un altro tipo di risorsa supportato.</span><span class="sxs-lookup"><span data-stu-id="9878e-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="9878e-114">I log di diagnostica a livello di risorsa è richiesto alcun agente e acquisire dati specifici delle risorse da hello piattaforma Azure stesso, i log di diagnostica a livello del sistema operativo guest acquisiscono i dati dal sistema operativo hello e applicazioni in esecuzione in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9878e-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="9878e-115">Non tutte le risorse supportano hello nuovo tipo di log di diagnostica risorse descritte di seguito.</span><span class="sxs-lookup"><span data-stu-id="9878e-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="9878e-116">Questo articolo contiene un elenco di sezione, quali tipi di risorse supportano hello nuovi a livello di risorsa log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="9878e-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="9878e-117">Log di diagnostica di risorsa e altri tipi di log</span><span class="sxs-lookup"><span data-stu-id="9878e-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="9878e-118">Possibili operazioni con i log di diagnostica a livello di risorsa</span><span class="sxs-lookup"><span data-stu-id="9878e-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="9878e-119">Ecco alcune delle operazioni di hello che è possibile eseguire con i log di diagnostica di risorse:</span><span class="sxs-lookup"><span data-stu-id="9878e-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Posizionamento logico dei log di diagnostica di risorsa](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="9878e-121">Salvarli tooa [ **Account di archiviazione** ](monitoring-archive-diagnostic-logs.md) per un controllo di controllo o manuale.</span><span class="sxs-lookup"><span data-stu-id="9878e-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="9878e-122">È possibile specificare hello memorizzazione tempo (in giorni) utilizzando **le impostazioni di diagnostica di risorse**.</span><span class="sxs-lookup"><span data-stu-id="9878e-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="9878e-123">[Trasmessi troppo**hub eventi** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) per l'inserimento di un servizio di terze parti o di una soluzione analitica personalizzato, ad esempio Power BI.</span><span class="sxs-lookup"><span data-stu-id="9878e-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="9878e-124">Analizzarli con [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="9878e-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="9878e-125">È possibile utilizzare un account di archiviazione o dello spazio dei nomi degli hub di eventi che non si trova in hello stessa sottoscrizione come hello una creazione di log.</span><span class="sxs-lookup"><span data-stu-id="9878e-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="9878e-126">utente di Hello che configura l'impostazione di hello deve disporre di sottoscrizioni di hello appropriate RBAC accesso tooboth.</span><span class="sxs-lookup"><span data-stu-id="9878e-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="9878e-127">Impostazioni di diagnostica di risorsa</span><span class="sxs-lookup"><span data-stu-id="9878e-127">Resource diagnostic settings</span></span>
<span data-ttu-id="9878e-128">I log di diagnostica per le non di calcolo vengono configurati tramite le impostazioni di diagnostica di risorsa.</span><span class="sxs-lookup"><span data-stu-id="9878e-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="9878e-129">Le **impostazioni di diagnostica di risorsa** permettono di controllare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="9878e-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="9878e-130">Destinazione dei log di diagnostica di risorsa e delle metriche, ad esempio un account di archiviazione, un Hub eventi e/o OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9878e-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="9878e-131">Categorie di log e metriche da inviare.</span><span class="sxs-lookup"><span data-stu-id="9878e-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="9878e-132">Periodo di tempo in cui ogni log di categoria deve essere mantenuto nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9878e-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="9878e-133">Un periodo di conservazione di zero giorni significa che i log vengono conservati all'infinito.</span><span class="sxs-lookup"><span data-stu-id="9878e-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="9878e-134">In caso contrario, il valore di hello può essere qualsiasi numero di giorni compreso tra 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="9878e-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="9878e-135">Se i criteri di conservazione sono impostati, ma l'archiviazione dei log in un Account di archiviazione è disabilitata (ad esempio, se solo le opzioni di hub eventi o OMS sono selezionate), i criteri di conservazione hello non hanno alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="9878e-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="9878e-136">Criteri di conservazione vengono applicati al giorno, vengono eliminati in modo a hello fine di un giorno (UTC), i log da giorno hello che si trova ora oltre i criteri di conservazione hello.</span><span class="sxs-lookup"><span data-stu-id="9878e-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="9878e-137">Ad esempio, se si dispone di un criterio di conservazione di un giorno, all'inizio di hello del giorno hello oggi hello registri hello ieri dovrebbero essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="9878e-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="9878e-138">Queste impostazioni vengono configurate facilmente tramite impostazioni di diagnostica per una risorsa nel portale di Azure hello hello, tramite i comandi di PowerShell di Azure e CLI o hello [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="9878e-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="9878e-139">I log di diagnostica e le metriche per dal livello di sistema operativo guest hello calcolo (ad esempio, le macchine virtuali o Service Fabric) sull'utilizzo delle risorse [un meccanismo separato per la selezione di output e di configurazione](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9878e-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="9878e-140">Come tooenable raccolta dei log di diagnostica di risorse</span><span class="sxs-lookup"><span data-stu-id="9878e-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="9878e-141">Raccolta dei log di diagnostica di risorse può essere abilitata [durante la creazione di una risorsa in un modello di gestione risorse di](./monitoring-enable-diagnostic-logs-using-template.md) o dopo la creazione di una risorsa dalla pagina della risorsa nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9878e-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="9878e-142">È anche possibile abilitare insieme in qualsiasi momento mediante i comandi di Azure PowerShell o l'interfaccia CLI o hello API REST di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9878e-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="9878e-143">Queste istruzioni potrebbero non essere applicabili direttamente tooevery risorse.</span><span class="sxs-lookup"><span data-stu-id="9878e-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="9878e-144">Vedere i collegamenti dello schema hello nella parte inferiore di hello di questa pagina toounderstand speciali i passaggi che possono applicare i tipi di risorsa toocertain.</span><span class="sxs-lookup"><span data-stu-id="9878e-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="9878e-145">Abilitare la raccolta dei log di diagnostica di risorsa nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="9878e-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="9878e-146">È possibile abilitare una raccolta di log di diagnostica di risorsa nel hello Azure portal dopo aver creata una risorsa da passare di risorsa specifico tooa o passando tooAzure Monitor.</span><span class="sxs-lookup"><span data-stu-id="9878e-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="9878e-147">tooenable questo tramite il monitoraggio di Azure:</span><span class="sxs-lookup"><span data-stu-id="9878e-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="9878e-148">In hello [portale di Azure](http://portal.azure.com)passare tooAzure Monitor e fare clic su **le impostazioni di diagnostica**</span><span class="sxs-lookup"><span data-stu-id="9878e-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="9878e-150">Se lo si desidera filtrare l'elenco hello in base al tipo di risorsa o gruppo di risorse, fare clic sul risorse hello per il quale si desidera tooset un'impostazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="9878e-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="9878e-151">Se nessuna impostazione esistano nella risorsa hello selezionata, verrà richiesta toocreate un'impostazione.</span><span class="sxs-lookup"><span data-stu-id="9878e-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="9878e-152">Fare clic su "Attiva diagnostica".</span><span class="sxs-lookup"><span data-stu-id="9878e-152">Click "Turn on diagnostics."</span></span>

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="9878e-154">Se sono presenti le impostazioni esistenti sulla risorsa hello, vedrai un elenco di impostazioni già configurato per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="9878e-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="9878e-155">Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).</span><span class="sxs-lookup"><span data-stu-id="9878e-155">Click "Add diagnostic setting."</span></span>

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="9878e-157">Assegnare un nome dell'impostazione, hello caselle di controllo per ogni toowhich destinazione desideri toosend dati e configurare la risorsa viene utilizzato per ogni destinazione.</span><span class="sxs-lookup"><span data-stu-id="9878e-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="9878e-158">Facoltativamente, impostare il numero di giorni tooretain questi log tramite hello **conservazione (giorni)** cursori (solo toohello applicabile account destinazione di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="9878e-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="9878e-159">La riserva di zero giorni registri hello vengono archiviati per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="9878e-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="9878e-161">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9878e-161">Click **Save**.</span></span>

<span data-ttu-id="9878e-162">Dopo alcuni istanti, hello nuova impostazione è visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica vengono inviati toohello specificato destinazioni appena nuovi dati di evento viene generati.</span><span class="sxs-lookup"><span data-stu-id="9878e-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="9878e-163">Abilitare la raccolta dei log di diagnostica di risorsa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9878e-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="9878e-164">raccolta di tooenable dei log di diagnostica di risorse tramite Azure PowerShell, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9878e-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="9878e-165">tooenable archiviazione dei log di diagnostica in un account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="9878e-166">archiviazione Hello ID dell'account è hello ID di risorsa per i registri hello toowhich di account di archiviazione desiderato toosend hello.</span><span class="sxs-lookup"><span data-stu-id="9878e-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="9878e-167">tooenable lo streaming di hub di eventi di log di diagnostica tooan, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="9878e-168">ID regola bus di servizio Hello è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="9878e-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="9878e-169">tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="9878e-170">È possibile ottenere l'ID di risorsa hello dell'area di lavoro Log Analitica utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9878e-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="9878e-171">È possibile combinare queste tooenable parametri più opzioni di output.</span><span class="sxs-lookup"><span data-stu-id="9878e-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="9878e-172">Abilitare la raccolta dei log di diagnostica di risorsa con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="9878e-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="9878e-173">raccolta tooenable dei log di diagnostica di risorse tramite hello CLI di Azure, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9878e-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="9878e-174">tooenable archiviazione dei log di diagnostica in un Account di archiviazione, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="9878e-175">archiviazione Hello ID dell'account è hello ID di risorsa per i registri hello toowhich di account di archiviazione desiderato toosend hello.</span><span class="sxs-lookup"><span data-stu-id="9878e-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="9878e-176">tooenable lo streaming di hub di eventi di log di diagnostica tooan, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="9878e-177">ID regola bus di servizio Hello è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="9878e-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="9878e-178">tooenable l'invio di log di diagnostica tooa Log Analitica dell'area di lavoro, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="9878e-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="9878e-179">È possibile combinare queste tooenable parametri più opzioni di output.</span><span class="sxs-lookup"><span data-stu-id="9878e-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="9878e-180">Abilitare la raccolta dei log di diagnostica di risorsa con l'API REST</span><span class="sxs-lookup"><span data-stu-id="9878e-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="9878e-181">le impostazioni di diagnostica toochange utilizzando hello API REST di monitoraggio di Azure, vedere [questo documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="9878e-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="9878e-182">Gestire le impostazioni di diagnostica di risorse nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="9878e-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="9878e-183">Verificare che tutte le risorse siano configurate con le impostazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="9878e-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="9878e-184">Passare troppo**monitoraggio** in hello portale e aprire **le impostazioni di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="9878e-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Pannello log diagnostico nel portale di hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="9878e-186">È possibile tooclick sezione di monitoraggio hello toofind "Più servizi".</span><span class="sxs-lookup"><span data-stu-id="9878e-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="9878e-187">Qui è possibile visualizzare e filtrare tutte le risorse che supportano le impostazioni di diagnostica toosee se dispongono di diagnostica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="9878e-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="9878e-188">È possibile eseguire il drill-down toosee se più vengono impostati su una risorsa e controllare quale account di archiviazione, spazio dei nomi di hub eventi, e/o area di lavoro Log Analitica per i dati vengono trasmessi.</span><span class="sxs-lookup"><span data-stu-id="9878e-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Risultati di Log di diagnostica nel portale](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="9878e-190">Aggiunta di che un'impostazione di diagnostica consente di visualizzare hello Visualizza impostazioni di diagnostica, in cui è possibile abilitare, disabilitare o modificare le impostazioni di diagnostica per hello selezionato risorse.</span><span class="sxs-lookup"><span data-stu-id="9878e-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="9878e-191">Servizi, categorie e schemi supportati per i log di diagnostica di risorsa</span><span class="sxs-lookup"><span data-stu-id="9878e-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="9878e-192">[Vedere l'articolo](monitoring-diagnostic-logs-schema.md) per un elenco completo dei servizi supportati e categorie log hello e schemi utilizzati da tali servizi.</span><span class="sxs-lookup"><span data-stu-id="9878e-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9878e-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9878e-193">Next steps</span></span>

* [<span data-ttu-id="9878e-194">I log di diagnostica di risorse di flusso troppo**hub eventi**</span><span class="sxs-lookup"><span data-stu-id="9878e-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="9878e-195">Modificare le impostazioni di diagnostica di risorse utilizzando l'API REST di Azure Monitor hello</span><span class="sxs-lookup"><span data-stu-id="9878e-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="9878e-196">Analizzare i log di Archiviazione di Azure con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9878e-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
