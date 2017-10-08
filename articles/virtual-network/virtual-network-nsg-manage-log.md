---
title: aaaMonitor operazioni, gli eventi e contatori per NSGs | Documenti Microsoft
description: Informazioni su come tooenable contatori, eventi e registrazione operativa per NSGs
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
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="e1200-103">Analisi dei log per i gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e1200-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="e1200-104">È possibile abilitare hello seguenti categorie di log di diagnostica per NSGs:</span><span class="sxs-lookup"><span data-stu-id="e1200-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="e1200-105">**Evento:** contiene voci per il gruppo le regole sono applicate tooVMs e i ruoli di istanza in base all'indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="e1200-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="e1200-106">lo stato di Hello per queste regole verrà raccolti ogni 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="e1200-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="e1200-107">**Contatore di regole:** contiene voci per quante volte ogni gruppo di regole viene applicata toodeny o consentire il traffico.</span><span class="sxs-lookup"><span data-stu-id="e1200-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="e1200-108">I log di diagnostica sono disponibili solo per NSGs distribuite tramite il modello di distribuzione del hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1200-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e1200-109">È possibile abilitare la registrazione diagnostica per NSGs distribuite tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="e1200-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="e1200-110">Per una migliore comprensione dei modelli di hello due, fare riferimento a hello [modelli di distribuzione Azure comprensione](../resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="e1200-111">La registrazione delle attività (precedentemente nota come controllo o registri operativi) è abilitata per impostazione predefinita per i gruppi di sicurezza di rete creati tramite qualsivoglia modello di distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1200-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="e1200-112">toodetermine quali operazioni sono state completate in NSGs nel registro attività hello, cercare le voci che contengono i seguenti tipi di risorsa hello:</span><span class="sxs-lookup"><span data-stu-id="e1200-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="e1200-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="e1200-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="e1200-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="e1200-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="e1200-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="e1200-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="e1200-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="e1200-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="e1200-117">Hello lettura [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn articolo ulteriori informazioni sui registri di attività.</span><span class="sxs-lookup"><span data-stu-id="e1200-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="e1200-118">Abilitare la registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="e1200-118">Enable diagnostic logging</span></span>

<span data-ttu-id="e1200-119">È necessario abilitare la registrazione diagnostica *ogni* NSG toocollect dati desiderata per.</span><span class="sxs-lookup"><span data-stu-id="e1200-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="e1200-120">Hello [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo spiega in cui è possibile inviare i log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="e1200-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="e1200-121">Se non si dispone di un gruppo esistente, hello completato i passaggi in hello [creare un gruppo di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md) toocreate articolo uno.</span><span class="sxs-lookup"><span data-stu-id="e1200-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="e1200-122">È possibile abilitare la registrazione utilizzando uno dei seguenti metodi hello diagnostica gruppo:</span><span class="sxs-lookup"><span data-stu-id="e1200-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e1200-123">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e1200-123">Azure portal</span></span>

<span data-ttu-id="e1200-124">registrazione toouse hello tooenable portale account di accesso toohello [portale](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1200-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="e1200-125">Fare clic su **Altri servizi**, quindi digitare *gruppi di sicurezza di rete*.</span><span class="sxs-lookup"><span data-stu-id="e1200-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="e1200-126">Selezionare gruppo che si desidera la registrazione per tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="e1200-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="e1200-127">Seguire le istruzioni di hello per le risorse non di calcolo in hello [abilitare i log di diagnostica nel portale di hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="e1200-128">Selezionare **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** o entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="e1200-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="e1200-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1200-129">PowerShell</span></span>

<span data-ttu-id="e1200-130">toouse PowerShell tooenable registrazione, seguire le istruzioni hello hello [abilitare i log di diagnostica tramite PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="e1200-131">Valutare le seguenti informazioni prima di immettere un comando dall'articolo hello hello:</span><span class="sxs-lookup"><span data-stu-id="e1200-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="e1200-132">È possibile determinare hello valore toouse per hello `-ResourceId` parametro sostituendo hello seguenti [testo], come appropriato, quindi immettere il comando hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="e1200-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="e1200-133">output di Hello ID comando hello simile troppo*/subscriptions/ [nome sottoscrizione Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="e1200-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="e1200-134">Se si desidera solo dati toocollect dalla categoria di log da aggiungere `-Categories [category]` toohello fine del comando di hello nell'articolo hello, in cui categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="e1200-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="e1200-135">Se non si utilizza hello `-Categories` parametro, la raccolta dei dati è abilitata per entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="e1200-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="e1200-136">interfaccia della riga di comando di Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="e1200-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="e1200-137">toouse hello registrazione tooenable CLI, seguire le istruzioni hello hello [abilitare i log di diagnostica tramite CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="e1200-138">Valutare le seguenti informazioni prima di immettere un comando dall'articolo hello hello:</span><span class="sxs-lookup"><span data-stu-id="e1200-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="e1200-139">È possibile determinare hello valore toouse per hello `-ResourceId` parametro sostituendo hello seguenti [testo], come appropriato, quindi immettere il comando hello `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="e1200-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="e1200-140">output di Hello ID comando hello simile troppo*/subscriptions/ [nome sottoscrizione Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="e1200-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="e1200-141">Se si desidera solo dati toocollect dalla categoria di log da aggiungere `-Categories [category]` toohello fine del comando di hello nell'articolo hello, in cui categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="e1200-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="e1200-142">Se non si utilizza hello `-Categories` parametro, la raccolta dei dati è abilitata per entrambe le categorie di log.</span><span class="sxs-lookup"><span data-stu-id="e1200-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="e1200-143">Dati registrati</span><span class="sxs-lookup"><span data-stu-id="e1200-143">Logged data</span></span>

<span data-ttu-id="e1200-144">Vengono scritti dati in formato JSON per entrambi i log.</span><span class="sxs-lookup"><span data-stu-id="e1200-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="e1200-145">dati specifici di Hello scritti per ogni tipo di log sono elencati in hello le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e1200-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="e1200-146">Registro eventi</span><span class="sxs-lookup"><span data-stu-id="e1200-146">Event log</span></span>
<span data-ttu-id="e1200-147">Questo log contiene informazioni su quale gruppo regole vengono applicate tooVMs e istanze del ruolo del servizio, in base all'indirizzo MAC del cloud.</span><span class="sxs-lookup"><span data-stu-id="e1200-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="e1200-148">dati di esempio seguenti Hello viene registrato per ogni evento:</span><span class="sxs-lookup"><span data-stu-id="e1200-148">hello following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="e1200-149">Log contatore regole</span><span class="sxs-lookup"><span data-stu-id="e1200-149">Rule counter log</span></span>

<span data-ttu-id="e1200-150">Questo log contiene informazioni su tooresources ogni regola applicata.</span><span class="sxs-lookup"><span data-stu-id="e1200-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="e1200-151">Hello dati di esempio seguente viene registrati ogni volta che viene applicata una regola:</span><span class="sxs-lookup"><span data-stu-id="e1200-151">hello following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="e1200-152">Visualizzare e analizzare i log</span><span class="sxs-lookup"><span data-stu-id="e1200-152">View and analyze logs</span></span>

<span data-ttu-id="e1200-153">toolearn come attività tooview registrare i dati, lettura hello [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="e1200-154">toolearn come dati, di log di diagnostica tooview leggere hello [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e1200-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="e1200-155">Se si invia dati di diagnostica tooLog Analitica, è possibile utilizzare hello [analitica gruppo di sicurezza di rete di Azure](../log-analytics/log-analytics-azure-networking-analytics.md) soluzione di gestione (anteprima) per approfondimenti avanzate.</span><span class="sxs-lookup"><span data-stu-id="e1200-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
