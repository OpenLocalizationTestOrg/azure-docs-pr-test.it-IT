---
title: Panoramica del routing di contenuti basato su URL | Documentazione Microsoft
description: Questa pagina fornisce una panoramica del routing di contenuti basato su URL del gateway applicazione, della configurazione UrlPathMap e della regola PathBasedRouting.
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="bbbe4-103">Panoramica del routing basato su percorso URL</span><span class="sxs-lookup"><span data-stu-id="bbbe4-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="bbbe4-104">Il routing basato su percorso URL consente di instradare il traffico a pool di server back-end in base ai percorsi URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="bbbe4-105">Uno degli scenari è l'instradamento delle richieste di tipi di contenuto diversi a pool di server back-end diversi.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="bbbe4-106">Nell'esempio seguente, il gateway applicazione soddisfa le richieste di traffico per contoso.com dai tre pool di server back-end, ad esempio VideoServerPool, ImageServerPool e DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="bbbe4-108">Le richieste per http://contoso.com/video* vengono instradate a VideoServerPool, mentre quelle per http://contoso.com/images* vengono instradate a ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="bbbe4-109">In caso di mancata corrispondenza dei percorsi, viene selezionato DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbbe4-110">Le regole vengono elaborate nell'ordine in cui sono elencate nel portale.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="bbbe4-111">È consigliabile configurare i listener multisito prima di configurare un listener di base.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="bbbe4-112">In questo modo il traffico viene indirizzato al back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="bbbe4-113">Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="bbbe4-114">Elemento di configurazione UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="bbbe4-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="bbbe4-115">L'elemento UrlPathMap consente di specificare modelli di percorso dei mapping dei pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="bbbe4-116">L'esempio di codice seguente è il frammento dell'elemento urlPathMap del file modello.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="bbbe4-117">PathPattern: questa impostazione è un elenco dei modelli di percorso usati per la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="bbbe4-118">Ognuno deve iniziare con una barra / e l'unica posizione in cui è consentito il carattere "*" è alla fine dopo "/".</span><span class="sxs-lookup"><span data-stu-id="bbbe4-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="bbbe4-119">La stringa inviata al selettore di percorsi non include alcun testo dopo il primo carattere "?" o "#" e questi caratteri non sono consentiti qui.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="bbbe4-120">Per altre informazioni, vedere un [modello di Azure Resource Manager che usa il routing basato su URL](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) .</span><span class="sxs-lookup"><span data-stu-id="bbbe4-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="bbbe4-121">Regola PathBasedRouting</span><span class="sxs-lookup"><span data-stu-id="bbbe4-121">PathBasedRouting rule</span></span>

<span data-ttu-id="bbbe4-122">RequestRoutingRule di tipo PathBasedRouting consente di associare un listener a un urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="bbbe4-123">Tutte le richieste ricevute per il listener vengono instradate in base ai criteri specificati in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="bbbe4-124">Frammento della regola PathBasedRouting:</span><span class="sxs-lookup"><span data-stu-id="bbbe4-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bbbe4-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bbbe4-125">Next steps</span></span>

<span data-ttu-id="bbbe4-126">Dopo aver acquisito familiarità con il routing di contenuti basato su URL, passare a [Create a Path-based rule for an application gateway by using the portal](application-gateway-create-url-route-portal.md) (Creare una regola basata sul percorso per un gateway applicazione usando il portale) per la creazione di un gateway applicazione con regole di routing basate su URL.</span><span class="sxs-lookup"><span data-stu-id="bbbe4-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
