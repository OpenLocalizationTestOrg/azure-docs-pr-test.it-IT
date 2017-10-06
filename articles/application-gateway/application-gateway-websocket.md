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
# <a name="overview-of-websocket-support-in-application-gateway"></a>Panoramica del supporto di WebSocket nel gateway dell'applicazione

Il gateway applicazione offre il supporto nativo per WebSocket in tutte le dimensioni di gateway. Non sussiste alcuna impostazione configurabile dall'utente tooselectively Abilita o disabilita il supporto di WebSocket. 

Il protocollo WebSocket standardizzato nella specifica [RFC6455](https://tools.ietf.org/html/rfc6455) consente una comunicazione full duplex tra un server e un client su una connessione TCP con esecuzione prolungata. Questa funzionalità consente una comunicazione più interattiva tra server web hello e client hello, che può essere bidirezionale senza necessità di hello per il polling come richiesto nelle implementazioni basate su HTTP. WebSocket sovraccarico è inferiore a differenza di HTTP e può riutilizzare hello stessa connessione TCP per più richieste/risposte risultante in un utilizzo più efficiente delle risorse. Protocolli di WebSocket sono progettate toowork attraverso le porte HTTP tradizionali di 80 e 443.

È possibile continuare a usare un listener HTTP standard nella porta 80 o 443 tooreceive traffico WebSocket. Il traffico di WebSocket è diretto toohello WebSocket attivato i server back-end usando pool back-end appropriata hello come specificato nelle regole di gateway applicazione. server di back-end Hello deve rispondere toohello probe di gateway applicazione, che sono descritte nel hello [Panoramica probe di integrità](application-gateway-probe-overview.md) sezione. I probe di integrità del gateway applicazione sono solo HTTP e HTTPS. Ogni server back-end deve rispondere tooHTTP probe per il server applicazioni gateway tooroute WebSocket traffico toohello.

## <a name="listener-configuration-element"></a>Elemento di configurazione del listener

Un listener HTTP esistente può essere utilizzato toosupport traffico WebSocket. Hello di seguito è riportato un frammento di un elemento listener HTTP da un file di modello di esempio. Si sarebbe necessario listener HTTP e HTTPS toosupport WebSocket e proteggere il traffico di WebSocket. Analogamente è possibile utilizzare hello [portale](application-gateway-create-gateway-portal.md) o [PowerShell](application-gateway-create-gateway-arm.md) toocreate un gateway applicazione con i listener nel traffico sulla porta 80/443 toosupport WebSocket.

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Configurazione di BackendAddressPool, BackendHttpSetting e della regola di routing

Un BackendAddressPool è toodefine utilizzato un pool di back-end con server WebSocket abilitato. backendHttpSetting Hello è definito con una back-end la porta 80 e 443. proprietà Hello basato su cookie di affinità e requestTimeouts non sono rilevanti tooWebSocket traffico. Nessuna modifica necessaria nella regola di routing hello, 'Basic' è utilizzato tootie hello listener appropriato toohello corrispondente pool di indirizzi back-end. 

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

## <a name="websocket-enabled-backend"></a>Back-end abilitato per WebSocket

Il back-end deve disporre di un server web HTTP/HTTPS in hello configurata la porta per WebSocket toowork (in genere 80/443). Questo requisito è il protocollo WebSocket richiede hello handshake iniziale toobe HTTP con il protocollo di aggiornamento tooWebSocket come un campo di intestazione. Hello Ecco un esempio di un'intestazione di:

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

Un altro motivo risiede nel fatto che il probe di integrità del back-end del gateway applicazione supporta solo i protocolli HTTP e HTTPS. Se il server di back-end hello non risponde tooHTTP o probe HTTPS, viene escluso dalla pool back-end.

## <a name="next-steps"></a>Passaggi successivi

Dopo avere imparare a supporto di WebSocket, andare troppo[creare un gateway applicazione](application-gateway-create-gateway.md) tooget avviato con un WebSocket l'applicazione web abilitata.

