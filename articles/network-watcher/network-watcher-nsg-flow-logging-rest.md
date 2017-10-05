---
title: Gestire i log di flusso del gruppo di sicurezza di rete con Network Watcher di Azure - API REST | Documentazione Microsoft
description: Questa pagina illustra come gestire i log di flusso del gruppo di sicurezza di rete in Network Watcher di Azure con l'API REST
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="0cd95-103">Configurazione dei log di flusso del gruppo di sicurezza di rete con l'API REST</span><span class="sxs-lookup"><span data-stu-id="0cd95-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0cd95-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0cd95-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="0cd95-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd95-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="0cd95-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="0cd95-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="0cd95-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="0cd95-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="0cd95-108">API REST</span><span class="sxs-lookup"><span data-stu-id="0cd95-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="0cd95-109">I log di flusso del gruppo di sicurezza di rete sono una funzionalità di Network Watcher che consente di visualizzare le informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="0cd95-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="0cd95-110">Sono scritti in formato JSON e mostrano i flussi in ingresso e in uscita in base a regole, scheda di rete a cui si applica il flusso, informazioni su 5 tuple relative al flusso (IP di origine/destinazione, porta di origine/destinazione, protocollo), e se il traffico è consentito o meno.</span><span class="sxs-lookup"><span data-stu-id="0cd95-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0cd95-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0cd95-111">Before you begin</span></span>

<span data-ttu-id="0cd95-112">ARMclient viene usato per chiamare l'API REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0cd95-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="0cd95-113">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="0cd95-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="0cd95-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="0cd95-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="0cd95-115">Per le chiamate dell'API REST di Network Watcher, il nome del gruppo di risorse nell'URI della richiesta è il gruppo di risorse che contiene Network Watcher, non le risorse su cui eseguono le azioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0cd95-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="0cd95-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="0cd95-116">Scenario</span></span>

<span data-ttu-id="0cd95-117">Lo scenario illustrato in questo articolo descrive come abilitare, disabilitare ed eseguire query sui log di flusso tramite l'API REST.</span><span class="sxs-lookup"><span data-stu-id="0cd95-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="0cd95-118">Per altre informazioni sui log di flusso del gruppo di sicurezza di rete, visitare [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md) (Log di flusso del gruppo di sicurezza di rete - Panoramica).</span><span class="sxs-lookup"><span data-stu-id="0cd95-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="0cd95-119">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="0cd95-119">In this scenario, you will:</span></span>

* <span data-ttu-id="0cd95-120">Abilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="0cd95-120">Enable flow logs</span></span>
* <span data-ttu-id="0cd95-121">Disabilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="0cd95-121">Disable flow logs</span></span>
* <span data-ttu-id="0cd95-122">Eseguire query per lo stato dei log di flusso</span><span class="sxs-lookup"><span data-stu-id="0cd95-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="0cd95-123">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="0cd95-123">Log in with ARMClient</span></span>

<span data-ttu-id="0cd95-124">Accedere ad armclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd95-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="0cd95-125">Registrare il provider di Insight</span><span class="sxs-lookup"><span data-stu-id="0cd95-125">Register Insights provider</span></span>

<span data-ttu-id="0cd95-126">Per il corretto funzionamento della registrazione dei flussi è necessario che il provider **Microsoft.Insights** sia registrato.</span><span class="sxs-lookup"><span data-stu-id="0cd95-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="0cd95-127">Per verificare che il provider **Microsoft.Insights** sia registrato, eseguire lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="0cd95-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="0cd95-128">Abilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0cd95-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="0cd95-129">L'esempio seguente mostra il comando che consente di abilitare i log di flusso:</span><span class="sxs-lookup"><span data-stu-id="0cd95-129">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="0cd95-130">La risposta restituita dall'esempio precedente è la seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd95-130">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="0cd95-131">Disabilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0cd95-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="0cd95-132">Usare l'esempio seguente per disabilitare i log di flusso.</span><span class="sxs-lookup"><span data-stu-id="0cd95-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="0cd95-133">La chiamata è uguale a quella usata per abilitare i log di flusso, ad eccezione di **false** che è impostato per la proprietà attivata.</span><span class="sxs-lookup"><span data-stu-id="0cd95-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="0cd95-134">La risposta restituita dall'esempio precedente è la seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd95-134">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="0cd95-135">Eseguire query sui log di flusso</span><span class="sxs-lookup"><span data-stu-id="0cd95-135">Query flow logs</span></span>

<span data-ttu-id="0cd95-136">La seguente chiamata REST esegue una query sullo stato dei log di flusso in un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="0cd95-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="0cd95-137">L'esempio seguente riporta la risposta restituita:</span><span class="sxs-lookup"><span data-stu-id="0cd95-137">The following is an example of the response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="0cd95-138">Scaricare un log di flusso</span><span class="sxs-lookup"><span data-stu-id="0cd95-138">Download a flow log</span></span>

<span data-ttu-id="0cd95-139">Il percorso di archiviazione di un log di flusso viene definito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="0cd95-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="0cd95-140">Uno strumento utile per accedere ai log di flusso salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="0cd95-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="0cd95-141">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd95-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="0cd95-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0cd95-142">Next steps</span></span>

<span data-ttu-id="0cd95-143">Informazioni su come [visualizzare i log di flusso con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0cd95-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="0cd95-144">Informazioni su come [visualizzare i log di flusso del gruppi di sicurezza di rete con strumenti open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="0cd95-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
