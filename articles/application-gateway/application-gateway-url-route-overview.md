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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="fa7be-103">Panoramica del routing basato su percorso URL</span><span class="sxs-lookup"><span data-stu-id="fa7be-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="fa7be-104">Routing basato su URL percorso consente di tooroute traffico tooback fine pool di server in base ai percorsi URL della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="fa7be-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="fa7be-105">Uno degli scenari di hello è tooroute richieste per i pool di server back-end toodifferent diversi tipi di contenuto.</span><span class="sxs-lookup"><span data-stu-id="fa7be-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="fa7be-106">Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com dai tre pool di server back-end, ad esempio: VideoServerPool ImageServerPool e DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="fa7be-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="fa7be-108">Le richieste per http://contoso.com/video * tooVideoServerPool indirizzato e http://contoso.com/images * tooImageServerPool indirizzato.</span><span class="sxs-lookup"><span data-stu-id="fa7be-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="fa7be-109">DefaultServerPool è selezionata se nessuno dei modelli di percorso hello corrisponde.</span><span class="sxs-lookup"><span data-stu-id="fa7be-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa7be-110">Le regole vengono elaborate in ordine di hello che sono elencati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="fa7be-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="fa7be-111">È tooconfiguring precedente prima tooconfigure consigliata multisito listener un listener di base.</span><span class="sxs-lookup"><span data-stu-id="fa7be-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="fa7be-112">In questo modo di terminare tale traffico Ottiene indirizzato toohello nuovo.</span><span class="sxs-lookup"><span data-stu-id="fa7be-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="fa7be-113">Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.</span><span class="sxs-lookup"><span data-stu-id="fa7be-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="fa7be-114">Elemento di configurazione UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="fa7be-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="fa7be-115">elemento urlPathMap Hello è mapping dei pool di server utilizzati toospecify percorso modelli tooback-end.</span><span class="sxs-lookup"><span data-stu-id="fa7be-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="fa7be-116">Hello esempio di codice seguente è hello frammento dell'elemento urlPathMap dal file di modello.</span><span class="sxs-lookup"><span data-stu-id="fa7be-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="fa7be-117">PathPattern: Questa impostazione è un elenco di toomatch modelli percorso.</span><span class="sxs-lookup"><span data-stu-id="fa7be-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="fa7be-118">Ogni deve iniziare con / e hello solo un "*" è consentita in hello fine successiva un "/".</span><span class="sxs-lookup"><span data-stu-id="fa7be-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="fa7be-119">stringa Hello inserito toohello matcher di percorso non include alcun testo dopo hello prima? o # e tali caratteri non consentiti.</span><span class="sxs-lookup"><span data-stu-id="fa7be-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="fa7be-120">Per altre informazioni, vedere un [modello di Azure Resource Manager che usa il routing basato su URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .</span><span class="sxs-lookup"><span data-stu-id="fa7be-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="fa7be-121">Regola PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="fa7be-121">PathBasedRouting rule</span></span>

<span data-ttu-id="fa7be-122">RequestRoutingRule di tipo PathBasedRouting è usato toobind urlPathMap di tooa un listener.</span><span class="sxs-lookup"><span data-stu-id="fa7be-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="fa7be-123">Tutte le richieste ricevute per il listener vengono instradate in base ai criteri specificati in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="fa7be-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="fa7be-124">Frammento della regola PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="fa7be-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fa7be-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa7be-125">Next steps</span></span>

<span data-ttu-id="fa7be-126">Dopo avere imparare routing contenuto basato su URL, andare troppo[creare un gateway applicazione utilizzando il routing basato su URL](application-gateway-create-url-route-portal.md) toocreate un gateway applicazione con le regole di routing di URL.</span><span class="sxs-lookup"><span data-stu-id="fa7be-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
