---
title: supporto aaaWebSocket in Gateway di applicazione di Azure | Documenti Microsoft
description: Questa pagina viene fornita una panoramica del supporto di WebSocket Gateway applicazione hello.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="a3dde-103">Panoramica del supporto di WebSocket nel gateway dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3dde-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="a3dde-104">Il gateway applicazione offre il supporto nativo per WebSocket in tutte le dimensioni di gateway.</span><span class="sxs-lookup"><span data-stu-id="a3dde-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="a3dde-105">Non sussiste alcuna impostazione configurabile dall'utente tooselectively Abilita o disabilita il supporto di WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a3dde-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="a3dde-106">Il protocollo WebSocket standardizzato nella specifica [RFC6455](https://tools.ietf.org/html/rfc6455) consente una comunicazione full duplex tra un server e un client su una connessione TCP con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="a3dde-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="a3dde-107">Questa funzionalità consente una comunicazione più interattiva tra server web hello e client hello, che può essere bidirezionale senza necessità di hello per il polling come richiesto nelle implementazioni basate su HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3dde-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="a3dde-108">WebSocket sovraccarico è inferiore a differenza di HTTP e può riutilizzare hello stessa connessione TCP per più richieste/risposte risultante in un utilizzo più efficiente delle risorse.</span><span class="sxs-lookup"><span data-stu-id="a3dde-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="a3dde-109">Protocolli di WebSocket sono progettate toowork attraverso le porte HTTP tradizionali di 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="a3dde-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="a3dde-110">È possibile continuare a usare un listener HTTP standard nella porta 80 o 443 tooreceive traffico WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a3dde-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="a3dde-111">Il traffico di WebSocket è diretto toohello WebSocket attivato i server back-end usando pool back-end appropriata hello come specificato nelle regole di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3dde-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="a3dde-112">server di back-end Hello deve rispondere toohello probe di gateway applicazione, che sono descritte nel hello [Panoramica probe di integrità](application-gateway-probe-overview.md) sezione.</span><span class="sxs-lookup"><span data-stu-id="a3dde-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="a3dde-113">I probe di integrità del gateway applicazione sono solo HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a3dde-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="a3dde-114">Ogni server back-end deve rispondere tooHTTP probe per il server applicazioni gateway tooroute WebSocket traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="a3dde-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="a3dde-115">Elemento di configurazione del listener</span><span class="sxs-lookup"><span data-stu-id="a3dde-115">Listener configuration element</span></span>

<span data-ttu-id="a3dde-116">Un listener HTTP esistente può essere utilizzato toosupport traffico WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a3dde-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="a3dde-117">Hello di seguito è riportato un frammento di un elemento listener HTTP da un file di modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="a3dde-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="a3dde-118">Si sarebbe necessario listener HTTP e HTTPS toosupport WebSocket e proteggere il traffico di WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a3dde-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="a3dde-119">Analogamente è possibile utilizzare hello [portale](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md) toocreate un gateway applicazione con i listener nel traffico sulla porta 80/443 toosupport WebSocket.</span><span class="sxs-lookup"><span data-stu-id="a3dde-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="a3dde-120">Configurazione di BackendAddressPool, BackendHttpSetting e della regola di routing</span><span class="sxs-lookup"><span data-stu-id="a3dde-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="a3dde-121">Un BackendAddressPool è toodefine utilizzato un pool di back-end con server WebSocket abilitato.</span><span class="sxs-lookup"><span data-stu-id="a3dde-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="a3dde-122">backendHttpSetting Hello è definito con una back-end la porta 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="a3dde-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="a3dde-123">proprietà Hello basato su cookie di affinità e requestTimeouts non sono rilevanti tooWebSocket traffico.</span><span class="sxs-lookup"><span data-stu-id="a3dde-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="a3dde-124">Nessuna modifica necessaria nella regola di routing hello, 'Basic' è utilizzato tootie hello listener appropriato toohello corrispondente pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="a3dde-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a><span data-ttu-id="a3dde-125">Back-end abilitato per WebSocket</span><span class="sxs-lookup"><span data-stu-id="a3dde-125">WebSocket enabled backend</span></span>

<span data-ttu-id="a3dde-126">Il back-end deve disporre di un server web HTTP/HTTPS in hello configurata la porta per WebSocket toowork (in genere 80/443).</span><span class="sxs-lookup"><span data-stu-id="a3dde-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="a3dde-127">Questo requisito è il protocollo WebSocket richiede hello handshake iniziale toobe HTTP con il protocollo di aggiornamento tooWebSocket come un campo di intestazione.</span><span class="sxs-lookup"><span data-stu-id="a3dde-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="a3dde-128">Hello Ecco un esempio di un'intestazione di:</span><span class="sxs-lookup"><span data-stu-id="a3dde-128">hello following is an example of a header:</span></span>

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

<span data-ttu-id="a3dde-129">Un altro motivo risiede nel fatto che il probe di integrità del back-end del gateway applicazione supporta solo i protocolli HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a3dde-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="a3dde-130">Se il server di back-end hello non risponde tooHTTP o probe HTTPS, viene escluso dalla pool back-end.</span><span class="sxs-lookup"><span data-stu-id="a3dde-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3dde-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3dde-131">Next steps</span></span>

<span data-ttu-id="a3dde-132">Dopo avere imparare a supporto di WebSocket, andare troppo[creare un gateway applicazione](application-gateway-create-gateway.md) tooget avviato con un WebSocket l'applicazione web abilitata.</span><span class="sxs-lookup"><span data-stu-id="a3dde-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

