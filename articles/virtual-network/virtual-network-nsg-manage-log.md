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
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Analisi dei log per i gruppi di sicurezza di rete

È possibile abilitare hello seguenti categorie di log di diagnostica per NSGs:

* **Evento:** contiene voci per il gruppo le regole sono applicate tooVMs e i ruoli di istanza in base all'indirizzo MAC. lo stato di Hello per queste regole verrà raccolti ogni 60 secondi.
* **Contatore di regole:** contiene voci per quante volte ogni gruppo di regole viene applicata toodeny o consentire il traffico.

> [!NOTE]
> I log di diagnostica sono disponibili solo per NSGs distribuite tramite il modello di distribuzione del hello Azure Resource Manager. È possibile abilitare la registrazione diagnostica per NSGs distribuite tramite il modello di distribuzione classica hello. Per una migliore comprensione dei modelli di hello due, fare riferimento a hello [modelli di distribuzione Azure comprensione](../resource-manager-deployment-model.md) articolo.

La registrazione delle attività (precedentemente nota come controllo o registri operativi) è abilitata per impostazione predefinita per i gruppi di sicurezza di rete creati tramite qualsivoglia modello di distribuzione di Azure. toodetermine quali operazioni sono state completate in NSGs nel registro attività hello, cercare le voci che contengono i seguenti tipi di risorsa hello: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Hello lettura [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) toolearn articolo ulteriori informazioni sui registri di attività. 

## <a name="enable-diagnostic-logging"></a>Abilitare la registrazione diagnostica

È necessario abilitare la registrazione diagnostica *ogni* NSG toocollect dati desiderata per. Hello [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo spiega in cui è possibile inviare i log di diagnostica. Se non si dispone di un gruppo esistente, hello completato i passaggi in hello [creare un gruppo di sicurezza di rete](virtual-networks-create-nsg-arm-pportal.md) toocreate articolo uno. È possibile abilitare la registrazione utilizzando uno dei seguenti metodi hello diagnostica gruppo:

### <a name="azure-portal"></a>Portale di Azure

registrazione toouse hello tooenable portale account di accesso toohello [portale](https://portal.azure.com). Fare clic su **Altri servizi**, quindi digitare *gruppi di sicurezza di rete*. Selezionare gruppo che si desidera la registrazione per tooenable hello. Seguire le istruzioni di hello per le risorse non di calcolo in hello [abilitare i log di diagnostica nel portale di hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo. Selezionare **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** o entrambe le categorie di log.

### <a name="powershell"></a>PowerShell

toouse PowerShell tooenable registrazione, seguire le istruzioni hello hello [abilitare i log di diagnostica tramite PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo. Valutare le seguenti informazioni prima di immettere un comando dall'articolo hello hello:

- È possibile determinare hello valore toouse per hello `-ResourceId` parametro sostituendo hello seguenti [testo], come appropriato, quindi immettere il comando hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. output di Hello ID comando hello simile troppo*/subscriptions/ [nome sottoscrizione Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Se si desidera solo dati toocollect dalla categoria di log da aggiungere `-Categories [category]` toohello fine del comando di hello nell'articolo hello, in cui categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*. Se non si utilizza hello `-Categories` parametro, la raccolta dei dati è abilitata per entrambe le categorie di log.

### <a name="azure-command-line-interface-cli"></a>interfaccia della riga di comando di Azure (CLI)

toouse hello registrazione tooenable CLI, seguire le istruzioni hello hello [abilitare i log di diagnostica tramite CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) articolo. Valutare le seguenti informazioni prima di immettere un comando dall'articolo hello hello:

- È possibile determinare hello valore toouse per hello `-ResourceId` parametro sostituendo hello seguenti [testo], come appropriato, quindi immettere il comando hello `azure network nsg show [resource-group-name] [nsg-name]`. output di Hello ID comando hello simile troppo*/subscriptions/ [nome sottoscrizione Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Se si desidera solo dati toocollect dalla categoria di log da aggiungere `-Categories [category]` toohello fine del comando di hello nell'articolo hello, in cui categoria è *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*. Se non si utilizza hello `-Categories` parametro, la raccolta dei dati è abilitata per entrambe le categorie di log.

## <a name="logged-data"></a>Dati registrati

Vengono scritti dati in formato JSON per entrambi i log. dati specifici di Hello scritti per ogni tipo di log sono elencati in hello le sezioni seguenti:

### <a name="event-log"></a>Registro eventi
Questo log contiene informazioni su quale gruppo regole vengono applicate tooVMs e istanze del ruolo del servizio, in base all'indirizzo MAC del cloud. dati di esempio seguenti Hello viene registrato per ogni evento:

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

### <a name="rule-counter-log"></a>Log contatore regole

Questo log contiene informazioni su tooresources ogni regola applicata. Hello dati di esempio seguente viene registrati ogni volta che viene applicata una regola:

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

## <a name="view-and-analyze-logs"></a>Visualizzare e analizzare i log

toolearn come attività tooview registrare i dati, lettura hello [Panoramica di hello Log attività Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo. toolearn come dati, di log di diagnostica tooview leggere hello [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articolo. Se si invia dati di diagnostica tooLog Analitica, è possibile utilizzare hello [analitica gruppo di sicurezza di rete di Azure](../log-analytics/log-analytics-azure-networking-analytics.md) soluzione di gestione (anteprima) per approfondimenti avanzate. 
