---
title: Gruppo di sicurezza di rete flusso registra aaaManage con Watcher di rete di Azure - CLI di Azure 1.0 | Documenti Microsoft
description: Questa pagina viene illustrato come gruppo di sicurezza di rete flusso toomanage accede Watcher di rete di Azure con Azure CLI 1.0
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
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="7f78b-103">Configurazione dei log di flusso del gruppo di sicurezza di rete con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="7f78b-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7f78b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7f78b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="7f78b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f78b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="7f78b-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="7f78b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="7f78b-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="7f78b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="7f78b-108">API REST</span><span class="sxs-lookup"><span data-stu-id="7f78b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="7f78b-109">I registri del flusso di gruppo di sicurezza di rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7f78b-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="7f78b-110">Questi registri di flusso sono scritti in formato json e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="7f78b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="7f78b-111">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="7f78b-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7f78b-112">Network Watcher usa attualmente l'interfaccia della riga di comando di Azure 1.0 per il supporto dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7f78b-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="7f78b-113">Registrare il provider di Insight</span><span class="sxs-lookup"><span data-stu-id="7f78b-113">Register Insights provider</span></span>

<span data-ttu-id="7f78b-114">Hello correttamente, in ordine per il flusso di registrazione toowork **Insights** provider deve essere registrato.</span><span class="sxs-lookup"><span data-stu-id="7f78b-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="7f78b-115">Se non si è certi se hello **Insights** provider è registrato, hello eseguire lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="7f78b-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="7f78b-116">Abilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="7f78b-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="7f78b-117">Hello comando tooenable flusso registri è illustrata nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7f78b-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="7f78b-118">Disabilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="7f78b-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="7f78b-119">Hello utilizzare log flusso toodisable di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7f78b-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="7f78b-120">Scaricare un log di flusso</span><span class="sxs-lookup"><span data-stu-id="7f78b-120">Download a Flow log</span></span>

<span data-ttu-id="7f78b-121">percorso di archiviazione Hello di un log di flusso è definito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="7f78b-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="7f78b-122">Tooaccess un utile strumento questi account di archiviazione di flusso salvare log tooa è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7f78b-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7f78b-123">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="7f78b-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="7f78b-124">Per informazioni sulla struttura di hello del log hello visitare [gruppo di sicurezza di rete flusso log Panoramica](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7f78b-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f78b-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f78b-125">Next Steps</span></span>

<span data-ttu-id="7f78b-126">Informazioni su come troppo[visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7f78b-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="7f78b-127">Informazioni su come troppo[visualizzare i log di flusso NSG con strumenti open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="7f78b-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
