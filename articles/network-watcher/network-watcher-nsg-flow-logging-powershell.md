---
title: Gestire i log di flusso del gruppo di sicurezza di rete con Network Watcher di Azure - PowerShell | Documentazione Microsoft
description: Questa pagina illustra come gestire i log di flusso del gruppo di sicurezza di rete in Network Watcher di Azure con PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9fa2e2e1c09b119bd2a1e149fd2cc080957af296
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="e8cdc-103">Configurazione dei log di flusso del gruppo di sicurezza di rete con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8cdc-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e8cdc-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e8cdc-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="e8cdc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8cdc-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="e8cdc-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="e8cdc-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="e8cdc-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="e8cdc-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="e8cdc-108">API REST</span><span class="sxs-lookup"><span data-stu-id="e8cdc-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="e8cdc-109">I log di flusso del gruppo di sicurezza di rete sono una funzionalità di Network Watcher che consente di visualizzare le informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e8cdc-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="e8cdc-110">Sono scritti in formato JSON e mostrano i flussi in ingresso e in uscita in base a regole, scheda di rete a cui si applica il flusso, informazioni su 5 tuple relative al flusso (IP di origine/destinazione, porta di origine/destinazione, protocollo), e se il traffico è consentito o meno.</span><span class="sxs-lookup"><span data-stu-id="e8cdc-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="e8cdc-111">Registrare il provider di Insight</span><span class="sxs-lookup"><span data-stu-id="e8cdc-111">Register Insights provider</span></span>

<span data-ttu-id="e8cdc-112">Per il corretto funzionamento della registrazione dei flussi è necessario che il provider **Microsoft.Insights** sia registrato.</span><span class="sxs-lookup"><span data-stu-id="e8cdc-112">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="e8cdc-113">Per verificare che il provider **Microsoft.Insights** sia registrato, eseguire lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="e8cdc-113">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="e8cdc-114">Abilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e8cdc-114">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="e8cdc-115">L'esempio seguente mostra il comando che consente di abilitare i log di flusso:</span><span class="sxs-lookup"><span data-stu-id="e8cdc-115">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="e8cdc-116">Disabilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e8cdc-116">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="e8cdc-117">Usare l'esempio seguente per disabilitare i log di flusso:</span><span class="sxs-lookup"><span data-stu-id="e8cdc-117">Use the following example to disable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="e8cdc-118">Scaricare un log di flusso</span><span class="sxs-lookup"><span data-stu-id="e8cdc-118">Download a Flow log</span></span>

<span data-ttu-id="e8cdc-119">Il percorso di archiviazione di un log di flusso viene definito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="e8cdc-119">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="e8cdc-120">Uno strumento utile per accedere ai log di flusso salvati in un account di archiviazione è Esplora archivi di Microsoft Azure, disponibile qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="e8cdc-120">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="e8cdc-121">Se viene specificato un account di archiviazione, i file di acquisizione di pacchetti vengono salvati in un account di archiviazione nel percorso seguente:</span><span class="sxs-lookup"><span data-stu-id="e8cdc-121">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="e8cdc-122">Per informazioni sulla struttura del log, leggere la [panoramica sul log di flusso del gruppo di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e8cdc-122">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8cdc-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8cdc-123">Next Steps</span></span>

<span data-ttu-id="e8cdc-124">Informazioni su come [visualizzare i log di flusso con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="e8cdc-124">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="e8cdc-125">Informazioni su come [visualizzare i log di flusso del gruppi di sicurezza di rete con strumenti open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="e8cdc-125">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>