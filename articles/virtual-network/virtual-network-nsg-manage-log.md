---
title: Monitorare operazioni, eventi e contatori per i gruppi di sicurezza di rete | Documentazione Microsoft
description: Informazioni su come abilitare la registrazione di contatori, eventi e operazioni per i gruppi di sicurezza di rete
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="a432c-103">Analisi dei log per i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="a432c-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="a432c-104">È possibile abilitare le seguenti categorie di log di diagnostica per i gruppi di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="a432c-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="a432c-105">**Evento:** contiene voci per cui le regole dei gruppi di sicurezza di rete sono applicate alle macchine virtuali e ai ruoli delle istanze in base all'indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="a432c-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="a432c-106">Lo stato di queste regole viene raccolto ogni 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="a432c-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="a432c-107">**Contenitore di regole:** contiene voci per sapere quante volte ogni regola dei gruppi di sicurezza di rete è stata applicata per rifiutare o consentire il traffico.</span><span class="sxs-lookup"><span data-stu-id="a432c-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="a432c-108">I log di diagnostica sono disponibili solo per i gruppi di sicurezza di rete distribuiti nel modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a432c-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="a432c-109">Non è possibile abilitare la registrazione diagnostica per i gruppi di sicurezza di rete distribuiti tramite il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="a432c-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="a432c-110">Per altre informazioni sui due modelli, vedere l'articolo [Comprendere i modelli di distribuzione di Azure](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a432c-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="a432c-111">La registrazione delle attività (precedentemente nota come controllo o registri operativi) è abilitata per impostazione predefinita per i gruppi di sicurezza di rete creati tramite qualsivoglia modello di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a432c-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="a432c-112">Per determinare quali operazioni sono state completate nei NGS nel log attività, cercare le voci che contengono i tipi di risorsa seguenti:</span><span class="sxs-lookup"><span data-stu-id="a432c-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="a432c-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="a432c-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="a432c-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="a432c-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="a432c-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="a432c-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="a432c-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="a432c-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="a432c-117">Leggere l'articolo [Panoramica del log attività di Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) per ulteriori informazioni sui log attività.</span><span class="sxs-lookup"><span data-stu-id="a432c-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="a432c-118">Abilitare la registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="a432c-118">Enable diagnostic logging</span></span>

<span data-ttu-id="a432c-119">Deve essere abilitata la registrazione diagnostica per *ogni* gruppo di sicurezza di rete da cui si vogliono raccogliere dati.</span><span class="sxs-lookup"><span data-stu-id="a432c-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="a432c-120">L'articolo [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) spiega dove è possibile inviare i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="a432c-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="a432c-121">Se non si dispone di un gruppo di sicurezza di rete esistente, completare i passaggi descritti nell'articolo [Creare un gruppo di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md) per crearne uno.</span><span class="sxs-lookup"><span data-stu-id="a432c-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="a432c-122">È possibile abilitare la registrazione diagnostica nei gruppi di sicurezza direte usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a432c-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a432c-123">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a432c-123">Azure portal</span></span>

<span data-ttu-id="a432c-124">Per usare li portale per abilitare la registrazione, accedere al [portale](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a432c-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="a432c-125">Fare clic su **Altri servizi**, quindi digitare *gruppi di sicurezza di rete*.</span><span class="sxs-lookup"><span data-stu-id="a432c-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="a432c-126">Selezionare il gruppo di sicurezza di rete per cui si vuole abilitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="a432c-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="a432c-127">Seguire le istruzioni per le risorse non di calcolo nell'articolo [Abilitare i log di diagnostica nel portale](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="a432c-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a432c-128">Selezionare **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** o entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="a432c-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="a432c-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a432c-129">PowerShell</span></span>

<span data-ttu-id="a432c-130">Per abilitare la registrazione con PowerShell, seguire le istruzioni nell'articolo [Abilitare i log di diagnostica tramite PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="a432c-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a432c-131">Valutare le seguenti informazioni prima di immettere un comando dall'articolo:</span><span class="sxs-lookup"><span data-stu-id="a432c-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="a432c-132">È possibile determinare il valore da usare per il parametro `-ResourceId` sostituendo in base alle necessità il [testo] seguente e quindi immettendo il comando `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="a432c-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="a432c-133">L'output dell'ID dal comando è simile a */subscriptions/[ID sottoscrizione]/resourceGroups/[Gruppo di risorse]/providers/Microsoft.Network/networkSecurityGroups/[Nome gruppo di sicurezza di rete]*.</span><span class="sxs-lookup"><span data-stu-id="a432c-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="a432c-134">Se si desidera solamente raccogliere i dati dalla categoria di log, aggiungere `-Categories [category]` alla fine del comando nell'articolo, dove la categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="a432c-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="a432c-135">Se non si usa il parametro `-Categories`, la raccolta dei dati viene abilitata per entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="a432c-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="a432c-136">interfaccia della riga di comando di Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="a432c-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="a432c-137">Per abilitare la registrazione con l'interfaccia della riga di comando, seguire le istruzioni nell'articolo [Abilitare i log di diagnostica tramite l'interfaccia della riga di comando](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="a432c-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="a432c-138">Valutare le seguenti informazioni prima di immettere un comando dall'articolo:</span><span class="sxs-lookup"><span data-stu-id="a432c-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="a432c-139">È possibile determinare il valore da usare per il parametro `-ResourceId` sostituendo in base alle necessità il [testo] seguente e quindi immettendo il comando `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="a432c-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="a432c-140">L'output dell'ID dal comando è simile a */subscriptions/[ID sottoscrizione]/resourceGroups/[Gruppo di risorse]/providers/Microsoft.Network/networkSecurityGroups/[Nome gruppo di sicurezza di rete]*.</span><span class="sxs-lookup"><span data-stu-id="a432c-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="a432c-141">Se si desidera solamente raccogliere i dati dalla categoria di log, aggiungere `-Categories [category]` alla fine del comando nell'articolo, dove la categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="a432c-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="a432c-142">Se non si usa il parametro `-Categories`, la raccolta dei dati viene abilitata per entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="a432c-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="a432c-143">Dati registrati</span><span class="sxs-lookup"><span data-stu-id="a432c-143">Logged data</span></span>

<span data-ttu-id="a432c-144">Vengono scritti dati in formato JSON per entrambi i log.</span><span class="sxs-lookup"><span data-stu-id="a432c-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="a432c-145">I dati specifici scritti per ciascun tipo di log sono elencati nelle sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a432c-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="a432c-146">Registro eventi</span><span class="sxs-lookup"><span data-stu-id="a432c-146">Event log</span></span>
<span data-ttu-id="a432c-147">Questo registro contiene informazioni su quali regole del gruppo di sicurezza di rete vengono applicate alle macchine virtuali e alle istanze del ruolo del servizio cloud, in base all'indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="a432c-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="a432c-148">I dati nell'esempio seguente vengono registrati per ogni evento:</span><span class="sxs-lookup"><span data-stu-id="a432c-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="a432c-149">Log contatore regole</span><span class="sxs-lookup"><span data-stu-id="a432c-149">Rule counter log</span></span>

<span data-ttu-id="a432c-150">Questo log contiene informazioni su ogni regola applicata alle risorse.</span><span class="sxs-lookup"><span data-stu-id="a432c-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="a432c-151">I dati nell'esempio seguente vengono registrati ogni volta che viene applicata una regola:</span><span class="sxs-lookup"><span data-stu-id="a432c-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="a432c-152">Visualizzare e analizzare i log</span><span class="sxs-lookup"><span data-stu-id="a432c-152">View and analyze logs</span></span>

<span data-ttu-id="a432c-153">Leggere l'articolo [Panoramica del log attività di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) per ulteriori informazioni su come visualizzare i dati del log attività.</span><span class="sxs-lookup"><span data-stu-id="a432c-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="a432c-154">Leggere l'articolo [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) per ulteriori informazioni su come visualizzare i dati dei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="a432c-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="a432c-155">Se si inviano dati di diagnostica a Log Analytics, è possibile usare la soluzione di gestione [Analisi di gruppo di sicurezza di rete di Azure](../log-analytics/log-analytics-azure-networking-analytics.md) (anteprima) per approfondimenti avanzati.</span><span class="sxs-lookup"><span data-stu-id="a432c-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
