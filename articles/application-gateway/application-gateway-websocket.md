---
title: Supporto di WebSocket nel gateway applicazione di Azure | Microsoft Docs
description: Questa pagina offre una panoramica del supporto di WebSocket nel gateway applicazione.
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="e2a26-103">Panoramica del supporto di WebSocket nel gateway dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e2a26-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="e2a26-104">Il gateway applicazione offre il supporto nativo per WebSocket in tutte le dimensioni di gateway.</span><span class="sxs-lookup"><span data-stu-id="e2a26-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="e2a26-105">Non esistono impostazioni configurabili dall'utente per abilitare o disabilitare in modo selettivo il supporto di WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="e2a26-106">Il protocollo WebSocket standardizzato nella specifica [RFC6455](https://tools.ietf.org/html/rfc6455) consente una comunicazione full duplex tra un server e un client su una connessione TCP con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="e2a26-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="e2a26-107">Questa funzionalità consente una comunicazione più interattiva tra il server Web e il client, che può essere bidirezionale senza che sia necessario il polling richiesto invece nelle implementazioni basate su HTTP.</span><span class="sxs-lookup"><span data-stu-id="e2a26-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="e2a26-108">A differenza del protocollo HTTP, WebSocket presenta un overhead ridotto e può riusare la stessa connessione TCP per più richieste/risposte garantendo così un utilizzo più efficiente delle risorse.</span><span class="sxs-lookup"><span data-stu-id="e2a26-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="e2a26-109">I protocolli WebSocket sono progettati per usare le porte HTTP 80 e 443 tradizionali.</span><span class="sxs-lookup"><span data-stu-id="e2a26-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="e2a26-110">È possibile continuare a usare un listener HTTP standard nella porta 80 o 443 per ricevere il traffico WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="e2a26-111">Il traffico WebSocket viene quindi indirizzato al server back-end abilitato per WebSocket usando il pool back-end appropriato, come specificato nelle regole del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2a26-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="e2a26-112">Il server back-end deve rispondere ai probe del gateway applicazione, descritti nella sezione di [panoramica dei probe di integrità](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2a26-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="e2a26-113">I probe di integrità del gateway applicazione sono solo HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e2a26-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="e2a26-114">Ogni server back-end deve rispondere a probe HTTP per il gateway applicazione per instradare il traffico WebSocket al server.</span><span class="sxs-lookup"><span data-stu-id="e2a26-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="e2a26-115">Elemento di configurazione del listener</span><span class="sxs-lookup"><span data-stu-id="e2a26-115">Listener configuration element</span></span>

<span data-ttu-id="e2a26-116">Per supportare il traffico WebSocket è possibile usare un listener HTTP esistente.</span><span class="sxs-lookup"><span data-stu-id="e2a26-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="e2a26-117">Di seguito è riportato il frammento dell'elemento httpListeners di un file modello di esempio.</span><span class="sxs-lookup"><span data-stu-id="e2a26-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="e2a26-118">Per supportare WebSocket e il traffico WebSocket sicuro saranno necessari listener sia HTTP che HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e2a26-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="e2a26-119">Per creare un gateway applicazione con listener sulla porta 80/443 per supportare il traffico WebSocket, è possibile usare in modo analogo il [portale](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e2a26-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="e2a26-120">Configurazione di BackendAddressPool, BackendHttpSetting e della regola di routing</span><span class="sxs-lookup"><span data-stu-id="e2a26-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="e2a26-121">BackendAddressPool viene usato per definire un pool back-end con server abilitati per WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="e2a26-122">backendHttpSetting è definito con una porta back-end 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="e2a26-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="e2a26-123">Le proprietà per l'affinità basata su cookie e requestTimeouts non sono rilevanti per il traffico WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="e2a26-124">Non è necessaria alcuna modifica nella regola di routing. Viene usato 'Basic' per collegare il listener appropriato al pool di indirizzi back-end corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e2a26-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="e2a26-125">Back-end abilitato per WebSocket</span><span class="sxs-lookup"><span data-stu-id="e2a26-125">WebSocket enabled backend</span></span>

<span data-ttu-id="e2a26-126">Per il funzionamento di WebSocket, è necessario che il back-end includa un server Web HTTP/HTTPS in esecuzione sulla porta configurata (in genere 80/443).</span><span class="sxs-lookup"><span data-stu-id="e2a26-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="e2a26-127">Il protocollo WebSocket richiede infatti un handshake iniziale HTTP con un campo di intestazione Upgrade per il protocollo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="e2a26-128">Di seguito è riportato un esempio di intestazione:</span><span class="sxs-lookup"><span data-stu-id="e2a26-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="e2a26-129">Un altro motivo risiede nel fatto che il probe di integrità del back-end del gateway applicazione supporta solo i protocolli HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e2a26-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="e2a26-130">Se il server back-end non risponde ai probe HTTP o HTTPS, il server viene escluso dal pool back-end.</span><span class="sxs-lookup"><span data-stu-id="e2a26-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2a26-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2a26-131">Next steps</span></span>

<span data-ttu-id="e2a26-132">Dopo aver acquisito familiarità con il supporto di WebSocket, [creare un gateway applicazione](application-gateway-create-gateway.md) per iniziare a usare un'applicazione Web abilitata per WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e2a26-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

