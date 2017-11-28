---
title: flusso del gruppo di sicurezza di rete aaaManage registra con Watcher di rete di Azure - API REST | Documenti Microsoft
description: Questa pagina viene illustrato come flusso del gruppo di sicurezza di rete toomanage accede Watcher di rete di Azure con l'API REST
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
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="c3100-103">Configurazione dei log di flusso del gruppo di sicurezza di rete con l'API REST</span><span class="sxs-lookup"><span data-stu-id="c3100-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c3100-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c3100-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="c3100-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3100-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="c3100-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="c3100-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="c3100-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="c3100-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="c3100-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c3100-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="c3100-109">I registri del flusso di gruppo di sicurezza di rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c3100-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="c3100-110">Questi registri di flusso sono scritti in formato json e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="c3100-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c3100-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c3100-111">Before you begin</span></span>

<span data-ttu-id="c3100-112">ARMclient è l'API REST di hello toocall utilizzati tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3100-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="c3100-113">ARMClient è reperibile in Chocolatey in [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) (ARMClient in Chocolatey)</span><span class="sxs-lookup"><span data-stu-id="c3100-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c3100-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="c3100-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="c3100-115">Per l'API REST di controllo rete chiamate hello Nome gruppo di risorse nella richiesta di hello che URI è gruppo di risorse hello contenente hello Watcher di rete, non le risorse hello si eseguono operazioni di diagnostica hello in.</span><span class="sxs-lookup"><span data-stu-id="c3100-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="c3100-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="c3100-116">Scenario</span></span>

<span data-ttu-id="c3100-117">scenario Hello illustrato in questo articolo viene illustrato come tooenable, disabilitare e query flusso i log usando hello API REST.</span><span class="sxs-lookup"><span data-stu-id="c3100-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="c3100-118">toolearn ulteriori informazioni su loggings flusso il gruppo di sicurezza di rete, visitare [registrazione flusso Network Security Group - Panoramica](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3100-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="c3100-119">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="c3100-119">In this scenario, you will:</span></span>

* <span data-ttu-id="c3100-120">Abilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="c3100-120">Enable flow logs</span></span>
* <span data-ttu-id="c3100-121">Disabilitare i log di flusso</span><span class="sxs-lookup"><span data-stu-id="c3100-121">Disable flow logs</span></span>
* <span data-ttu-id="c3100-122">Eseguire query per lo stato dei log di flusso</span><span class="sxs-lookup"><span data-stu-id="c3100-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c3100-123">Accedere con ARMClient</span><span class="sxs-lookup"><span data-stu-id="c3100-123">Log in with ARMClient</span></span>

<span data-ttu-id="c3100-124">Accedi tooarmclient con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3100-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="c3100-125">Registrare il provider di Insight</span><span class="sxs-lookup"><span data-stu-id="c3100-125">Register Insights provider</span></span>

<span data-ttu-id="c3100-126">Hello correttamente, in ordine per il flusso di registrazione toowork **Insights** provider deve essere registrato.</span><span class="sxs-lookup"><span data-stu-id="c3100-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="c3100-127">Se non si è certi se hello **Insights** provider è registrato, hello eseguire lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="c3100-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="c3100-128">Abilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c3100-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="c3100-129">Hello comando tooenable flusso registri è illustrata nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c3100-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="c3100-130">Hello ha restituito una risposta hello precedente esempio è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c3100-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="c3100-131">Disabilitare i log di flusso dei gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c3100-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="c3100-132">Registra hello utilizzare flusso toodisable riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c3100-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="c3100-133">Hello è chiamata hello stesso come abilitare i registri di flusso, ad eccezione di **false** è impostato per la proprietà hello abilitato.</span><span class="sxs-lookup"><span data-stu-id="c3100-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="c3100-134">Hello ha restituito una risposta hello precedente esempio è il seguente:</span><span class="sxs-lookup"><span data-stu-id="c3100-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="c3100-135">Eseguire query sui log di flusso</span><span class="sxs-lookup"><span data-stu-id="c3100-135">Query flow logs</span></span>

<span data-ttu-id="c3100-136">Hello in seguito a chiamata REST query hello lo stato del flusso di log in un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c3100-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="c3100-137">Hello Ecco un esempio di risposta hello restituito:</span><span class="sxs-lookup"><span data-stu-id="c3100-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="c3100-138">Scaricare un log di flusso</span><span class="sxs-lookup"><span data-stu-id="c3100-138">Download a flow log</span></span>

<span data-ttu-id="c3100-139">percorso di archiviazione Hello di un log di flusso è definito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="c3100-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="c3100-140">Tooaccess un utile strumento questi account di archiviazione di flusso salvare log tooa è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="c3100-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="c3100-141">Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="c3100-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="c3100-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3100-142">Next steps</span></span>

<span data-ttu-id="c3100-143">Informazioni su come troppo[visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="c3100-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="c3100-144">Informazioni su come troppo[visualizzare i log di flusso NSG con strumenti open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="c3100-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
