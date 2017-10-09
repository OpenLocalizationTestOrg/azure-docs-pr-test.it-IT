---
title: Panoramica del routing del contenuto basato su aaaURL | Documenti Microsoft
description: Questa pagina viene fornita una panoramica del routing di hello applicazione Gateway URL basato sul contenuto, UrlPathMap configurazione e della regola PathBasedRouting.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>Panoramica del routing basato su percorso URL

Routing basato su URL percorso consente di tooroute traffico tooback fine pool di server in base ai percorsi URL della richiesta di hello. 

Uno degli scenari di hello è tooroute richieste per i pool di server back-end toodifferent diversi tipi di contenuto.

Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com dai tre pool di server back-end, ad esempio: VideoServerPool ImageServerPool e DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Le richieste per http://contoso.com/video * tooVideoServerPool indirizzato e http://contoso.com/images * tooImageServerPool indirizzato. DefaultServerPool è selezionata se nessuno dei modelli di percorso hello corrisponde.

> [!IMPORTANT]
> Le regole vengono elaborate in ordine di hello che sono elencati nel portale di hello. È tooconfiguring precedente prima tooconfigure consigliata multisito listener un listener di base.  In questo modo di terminare tale traffico Ottiene indirizzato toohello nuovo. Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.

## <a name="urlpathmap-configuration-element"></a>Elemento di configurazione UrlPathMap

elemento urlPathMap Hello è mapping dei pool di server utilizzati toospecify percorso modelli tooback-end. Hello esempio di codice seguente è hello frammento dell'elemento urlPathMap dal file di modello.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: Questa impostazione è un elenco di toomatch modelli percorso. Ogni deve iniziare con / e hello solo un "*" è consentita in hello fine successiva un "/". stringa Hello inserito toohello matcher di percorso non include alcun testo dopo hello prima? o # e tali caratteri non consentiti.

Per altre informazioni, vedere un [modello di Azure Resource Manager che usa il routing basato su URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .

## <a name="pathbasedrouting-rule"></a>Regola PathBasedRouting

RequestRoutingRule di tipo PathBasedRouting è usato toobind urlPathMap di tooa un listener. Tutte le richieste ricevute per il listener vengono instradate in base ai criteri specificati in urlPathMap.
Frammento della regola PathBasedRouting:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Passaggi successivi

Dopo avere imparare routing contenuto basato su URL, andare troppo[creare un gateway applicazione utilizzando il routing basato su URL](application-gateway-create-url-route-portal.md) toocreate un gateway applicazione con le regole di routing di URL.
