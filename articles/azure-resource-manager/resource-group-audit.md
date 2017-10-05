---
title: "Visualizzare i log attività di Azure per monitorare le risorse | Documentazione Microsoft"
description: "Usare i log attività per esaminare le azioni degli utenti e gli errori. Mostra il portale di Azure, PowerShell, l'interfaccia della riga di comando di Azure e REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="65d30-104">Visualizzare i log attività per controllare le azioni sulle risorse</span><span class="sxs-lookup"><span data-stu-id="65d30-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="65d30-105">Con i log attività è possibile determinare:</span><span class="sxs-lookup"><span data-stu-id="65d30-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="65d30-106">le operazioni eseguite sulle risorse nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="65d30-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="65d30-107">chi ha avviato l'operazione (anche se le operazioni avviate da un servizio back-end non restituiscono un utente come chiamante);</span><span class="sxs-lookup"><span data-stu-id="65d30-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="65d30-108">quando si è verificata l'operazione;</span><span class="sxs-lookup"><span data-stu-id="65d30-108">when the operation occurred</span></span>
* <span data-ttu-id="65d30-109">lo stato dell'operazione;</span><span class="sxs-lookup"><span data-stu-id="65d30-109">the status of the operation</span></span>
* <span data-ttu-id="65d30-110">i valori delle altre proprietà che potrebbero essere utili per esaminare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="65d30-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="65d30-111">È possibile recuperare le informazioni dai log attività tramite il portale, PowerShell, l'interfaccia della riga di comando di Azure, l'API REST di Insights o la [libreria .NET di Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="65d30-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="65d30-112">Portale</span><span class="sxs-lookup"><span data-stu-id="65d30-112">Portal</span></span>
1. <span data-ttu-id="65d30-113">Per visualizzare i log attività dal portale, selezionare **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="65d30-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![Selezionare i log di attività](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="65d30-115">In alternativa, per filtrare automaticamente il log attività per una determinata risorsa o uno specifico gruppo di risorse, selezionare **Log attività** nel pannello di tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="65d30-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="65d30-116">Si noti che il log attività viene automaticamente filtrato in base alla risorsa selezionata.</span><span class="sxs-lookup"><span data-stu-id="65d30-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![filtrare in base alla risorsa](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="65d30-118">Nel pannello **Log attività** viene visualizzato un riepilogo delle operazioni recenti.</span><span class="sxs-lookup"><span data-stu-id="65d30-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![visualizzare le azioni](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="65d30-120">Per limitare il numero di operazioni visualizzate, selezionare condizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="65d30-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="65d30-121">Ad esempio, l'immagine seguente mostra i campi **Intervallo di tempo** ed **Evento avviato da** modificati per poter visualizzare le azioni eseguite da un determinato utente o applicazione il mese scorso.</span><span class="sxs-lookup"><span data-stu-id="65d30-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="65d30-122">Selezionare **Applica** per visualizzare i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="65d30-122">Select **Apply** to view the results of your query.</span></span>
   
    ![impostare le opzioni di filtro](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="65d30-124">Se è necessario eseguire ancora la query in un secondo momento, selezionare **Salva** e assegnare un nome alla query.</span><span class="sxs-lookup"><span data-stu-id="65d30-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![Salvare la query](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="65d30-126">Per eseguire rapidamente una query, è possibile selezionare una query predefinita, ad esempio "distribuzioni non riuscite".</span><span class="sxs-lookup"><span data-stu-id="65d30-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![Selezionare la query](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="65d30-128">La query selezionata imposta automaticamente i valori di filtro necessari.</span><span class="sxs-lookup"><span data-stu-id="65d30-128">The selected query automatically sets the required filter values.</span></span>

    ![Visualizzare gli errori di distribuzione](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="65d30-130">Selezionare una delle operazioni per visualizzare un riepilogo dell'evento.</span><span class="sxs-lookup"><span data-stu-id="65d30-130">Select one of the operations to see a summary of the event.</span></span>

    ![Visualizzare l'operazione](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="65d30-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65d30-132">PowerShell</span></span>
1. <span data-ttu-id="65d30-133">Per recuperare le voci di log, eseguire il comando **Get-AzureRmLog** .</span><span class="sxs-lookup"><span data-stu-id="65d30-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="65d30-134">Offrire parametri aggiuntivi per filtrare l'elenco di voci.</span><span class="sxs-lookup"><span data-stu-id="65d30-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="65d30-135">Se non si specifica un'ora di inizio e fine, vengono restituite le voci per l'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="65d30-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="65d30-136">Ad esempio, per recuperare le operazioni per un gruppo di risorse durante l'ultima ora, eseguire:</span><span class="sxs-lookup"><span data-stu-id="65d30-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="65d30-137">L'esempio seguente illustra come usare il log attività per cercare le operazioni eseguite durante un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="65d30-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="65d30-138">Le date di inizio e fine vengono specificate in un formato Data.</span><span class="sxs-lookup"><span data-stu-id="65d30-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="65d30-139">In alternativa, è possibile usare funzioni data per specificare l'intervallo di date, ad esempio gli ultimi 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="65d30-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="65d30-140">A seconda dell'ora di inizio specificata, il comando precedente può restituire un lungo elenco di operazioni per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="65d30-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="65d30-141">I risultati possono essere filtrati in base all'elemento da cercare specificando i criteri di ricerca.</span><span class="sxs-lookup"><span data-stu-id="65d30-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="65d30-142">Se si vuole capire il motivo per cui un'app Web è stata arrestata, ad esempio, è possibile eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="65d30-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="65d30-143">In questo esempio indica che è stata eseguita un'azione di arresto da someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="65d30-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="65d30-144">È possibile cercare le azioni eseguite da un utente specifico, anche per un gruppo di risorse che non esiste più.</span><span class="sxs-lookup"><span data-stu-id="65d30-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="65d30-145">È possibile filtrare le operazioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="65d30-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="65d30-146">È possibile concentrarsi su un errore esaminando il messaggio di stato per tale voce.</span><span class="sxs-lookup"><span data-stu-id="65d30-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="65d30-147">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="65d30-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="65d30-148">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="65d30-148">Azure CLI</span></span>
* <span data-ttu-id="65d30-149">Per recuperare le voci di log, eseguire il comando **azure group log show** .</span><span class="sxs-lookup"><span data-stu-id="65d30-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="65d30-150">API REST</span><span class="sxs-lookup"><span data-stu-id="65d30-150">REST API</span></span>
<span data-ttu-id="65d30-151">Le operazioni REST per l'uso del log attività fanno parte delle [Informazioni di riferimento sulle API REST di Azure Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="65d30-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="65d30-152">Per recuperare gli eventi del log attività, vedere [Elencare gli eventi di gestione in una sottoscrizione](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="65d30-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65d30-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65d30-153">Next steps</span></span>
* <span data-ttu-id="65d30-154">I log attività di Azure possono essere usati con Power BI per ottenere altre informazioni sulle azioni nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="65d30-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="65d30-155">Vedere [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Visualizzare e analizzare i log attività di Azure in Power BI e altri strumenti).</span><span class="sxs-lookup"><span data-stu-id="65d30-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="65d30-156">Per informazioni su come impostare i criteri di sicurezza, vedere [Controllo degli accessi in base al ruolo in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="65d30-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="65d30-157">Per informazioni sui comandi per visualizzare le operazioni di distribuzione, vedere [Visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="65d30-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="65d30-158">Per informazioni su come impedire operazioni di eliminazione su una risorsa per tutti gli utenti, vedere [Bloccare le risorse con Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="65d30-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

