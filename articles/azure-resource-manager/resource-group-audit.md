---
title: "attività di Azure aaaView registra risorse toomonitor | Documenti Microsoft"
description: "Utilizzare hello attività registra errori e tooreview azioni dell'utente. Mostra il portale di Azure, PowerShell, l'interfaccia della riga di comando di Azure e REST."
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
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="aeb62-104">Visualizza attività registra le azioni tooaudit sulle risorse</span><span class="sxs-lookup"><span data-stu-id="aeb62-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="aeb62-105">Con i log attività è possibile determinare:</span><span class="sxs-lookup"><span data-stu-id="aeb62-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="aeb62-106">le operazioni eseguite sulle risorse hello nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="aeb62-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="aeb62-107">che ha avviato l'operazione di hello (anche se le operazioni avviate da un servizio back-end non restituiscono un utente come chiamante hello)</span><span class="sxs-lookup"><span data-stu-id="aeb62-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="aeb62-108">Quando si è verificato il funzionamento di hello</span><span class="sxs-lookup"><span data-stu-id="aeb62-108">when hello operation occurred</span></span>
* <span data-ttu-id="aeb62-109">stato Hello dell'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="aeb62-109">hello status of hello operation</span></span>
* <span data-ttu-id="aeb62-110">i valori Hello altre proprietà che potrebbero facilitare la ricerca operazione hello</span><span class="sxs-lookup"><span data-stu-id="aeb62-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="aeb62-111">È possibile recuperare informazioni dal log attività hello tramite il portale di hello, PowerShell, CLI di Azure, l'API REST di Insights o [libreria .NET di Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="aeb62-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="aeb62-112">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aeb62-112">Portal</span></span>
1. <span data-ttu-id="aeb62-113">Selezionare i log di attività hello tooview tramite il portale di hello **monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="aeb62-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![Selezionare i log di attività](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="aeb62-115">O, nel log attività di hello tooautomatically filtro per una determinata risorsa o un gruppo di risorse, seleziona **log attività** da tale pannello della risorsa.</span><span class="sxs-lookup"><span data-stu-id="aeb62-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="aeb62-116">Si noti che log attività hello vengono filtrati automaticamente dalla risorsa hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="aeb62-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![filtrare in base alla risorsa](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="aeb62-118">In hello **Log attività** pannello viene visualizzato un riepilogo delle operazioni recenti.</span><span class="sxs-lookup"><span data-stu-id="aeb62-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![visualizzare le azioni](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="aeb62-120">numero di hello toorestrict di operazioni visualizzata, selezionare condizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="aeb62-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="aeb62-121">Ad esempio, hello seguente immagine Mostra hello **Timespan** e **evento avviato da** campi modificati azioni di hello tooview da un particolare utente o applicazione per hello mese scorso.</span><span class="sxs-lookup"><span data-stu-id="aeb62-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="aeb62-122">Selezionare **applica** risultati hello tooview della query.</span><span class="sxs-lookup"><span data-stu-id="aeb62-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![impostare le opzioni di filtro](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="aeb62-124">Se è necessario query hello toorun in un secondo momento, selezionare **salvare** e assegnare un nome di query hello.</span><span class="sxs-lookup"><span data-stu-id="aeb62-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![Salvare la query](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="aeb62-126">tooquickly eseguire una query, è possibile selezionare una delle query incorporato hello, ad esempio distribuzioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="aeb62-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![Selezionare la query](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="aeb62-128">la query selezionata Hello imposta automaticamente i valori di filtro hello necessario.</span><span class="sxs-lookup"><span data-stu-id="aeb62-128">hello selected query automatically sets hello required filter values.</span></span>

    ![Visualizzare gli errori di distribuzione](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="aeb62-130">Selezionare una delle operazioni di hello toosee un riepilogo dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="aeb62-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![Visualizzare l'operazione](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="aeb62-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aeb62-132">PowerShell</span></span>
1. <span data-ttu-id="aeb62-133">le voci di log tooretrieve, eseguire hello **Get AzureRmLog** comando.</span><span class="sxs-lookup"><span data-stu-id="aeb62-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="aeb62-134">Fornire parametri aggiuntivi toofilter hello elenco voci.</span><span class="sxs-lookup"><span data-stu-id="aeb62-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="aeb62-135">Se non si specifica un'ora di inizio e fine, vengono restituite le voci per hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="aeb62-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="aeb62-136">Ad esempio, eseguire le operazioni di hello tooretrieve per un gruppo di risorse durante l'ultima ora hello:</span><span class="sxs-lookup"><span data-stu-id="aeb62-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="aeb62-137">Hello di esempio seguente viene illustrato come attività hello toouse log tooresearch operazioni eseguite durante un tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="aeb62-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="aeb62-138">date di inizio e fine Hello vengono specificate in un formato di Data.</span><span class="sxs-lookup"><span data-stu-id="aeb62-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="aeb62-139">In alternativa, è possibile utilizzare funzioni toospecify hello data intervallo di date, ad esempio hello ultimi 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="aeb62-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="aeb62-140">In base all'ora di inizio hello specificate, i comandi precedenti hello possono restituire un lungo elenco di operazioni per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="aeb62-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="aeb62-141">È possibile filtrare i risultati di hello per ciò che si sta cercando, fornendo i criteri di ricerca.</span><span class="sxs-lookup"><span data-stu-id="aeb62-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="aeb62-142">Se si sta tentando di tooresearch come un'app web è stata arrestata, ad esempio, è possibile eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aeb62-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="aeb62-143">In questo esempio indica che è stata eseguita un'azione di arresto da someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="aeb62-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="aeb62-144">È possibile esaminare le azioni di hello intraprese da un particolare utente, anche per un gruppo di risorse che non esiste più.</span><span class="sxs-lookup"><span data-stu-id="aeb62-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="aeb62-145">È possibile filtrare le operazioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="aeb62-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="aeb62-146">È possibile concentrarsi su un errore esaminando il messaggio di stato hello per tale voce.</span><span class="sxs-lookup"><span data-stu-id="aeb62-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="aeb62-147">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="aeb62-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="aeb62-148">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="aeb62-148">Azure CLI</span></span>
* <span data-ttu-id="aeb62-149">le voci del registro tooretrieve eseguire hello **gruppo azure log Mostra** comando.</span><span class="sxs-lookup"><span data-stu-id="aeb62-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="aeb62-150">API REST</span><span class="sxs-lookup"><span data-stu-id="aeb62-150">REST API</span></span>
<span data-ttu-id="aeb62-151">le operazioni REST Hello per l'utilizzo di log attività hello fanno parte di hello [API REST di Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="aeb62-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="aeb62-152">tooretrieve attività log eventi, vedere [elenco eventi di gestione di hello in una sottoscrizione](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="aeb62-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb62-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aeb62-153">Next steps</span></span>
* <span data-ttu-id="aeb62-154">Log attività Azure è utilizzabile con Power BI toogain maggiori informazioni relative sulle azioni di hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="aeb62-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="aeb62-155">Vedere [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Visualizzare e analizzare i log attività di Azure in Power BI e altri strumenti).</span><span class="sxs-lookup"><span data-stu-id="aeb62-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="aeb62-156">toolearn sull'impostazione di criteri di sicurezza, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="aeb62-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="aeb62-157">toolearn sui comandi hello per la visualizzazione delle operazioni di distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="aeb62-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="aeb62-158">toolearn tooprevent eliminazioni su una risorsa per tutti gli utenti, vedere [bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="aeb62-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

