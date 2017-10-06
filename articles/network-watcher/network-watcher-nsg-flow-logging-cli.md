---
title: Gruppo di sicurezza di rete flusso registra aaaManage con Watcher di rete di Azure - CLI di Azure | Documenti Microsoft
description: Questa pagina viene illustrato come gruppo di sicurezza di rete flusso toomanage accede Watcher di rete di Azure con CLI di Azure
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Configurazione dei log di flusso del gruppo di sicurezza di rete con l'interfaccia della riga di comando di Azure

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

I registri del flusso di gruppo di sicurezza di rete sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete. Questi registri di flusso sono scritti in formato json e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.

In questo articolo utilizza la nuova generazione CLI per modello di distribuzione Gestione risorse hello, CLI di Azure 2.0, che è disponibile per Windows, Mac e Linux.

hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="register-insights-provider"></a>Registrare il provider di Insight

Hello correttamente, in ordine per il flusso di registrazione toowork **Insights** provider deve essere registrato. Se non si è certi se hello **Insights** provider è registrato, hello eseguire lo script seguente.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Abilitare i log di flusso dei gruppi di sicurezza di rete

Hello comando tooenable flusso registri è illustrata nell'esempio seguente hello:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>Disabilitare i log di flusso dei gruppi di sicurezza di rete

Hello utilizzare log flusso toodisable di esempio seguente:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a>Scaricare un log di flusso

percorso di archiviazione Hello di un log di flusso è definito al momento della creazione. Tooaccess un utile strumento questi account di archiviazione di flusso salvare log tooa è Microsoft Azure Storage Explorer, che può essere scaricata qui: http://storageexplorer.com/

Se viene specificato un account di archiviazione, i file di acquisizione dei pacchetti vengono salvati tooa account di archiviazione in hello seguente posizione:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Per informazioni sulla struttura di hello del log hello visitare [gruppo di sicurezza di rete flusso log Panoramica](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[visualizzare i log di flusso NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Informazioni su come troppo[visualizzare i log di flusso NSG con strumenti open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
