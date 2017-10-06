---
title: "aaaHosting più siti in Gateway di applicazione di Azure | Documenti Microsoft"
description: "Questa pagina viene fornita una panoramica del supporto di più siti di Gateway applicazione hello."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Hosting di più siti in un gateway applicazione

Hosting di più siti consente tooconfigure più di una sola applicazione web su hello stessa istanza di gateway applicazione. Questa funzionalità permette di tooconfigure una topologia più efficiente per le distribuzioni tramite l'aggiunta di gateway applicazione tooone di too20 siti Web. Ogni sito Web può essere indirizzato tooits proprietari pool back-end. Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com da due pool di server back-end denominato ContosoServerPool e FabrikamServerPool.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Le regole vengono elaborate in ordine di hello che sono elencati nel portale di hello. È tooconfiguring precedente prima tooconfigure consigliata multisito listener un listener di base.  In questo modo di terminare tale traffico Ottiene indirizzato toohello nuovo. Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.

Le richieste per http://contoso.com tooContosoServerPool indirizzato e http://fabrikam.com tooFabrikamServerPool indirizzato.

Analogamente, due sottodomini di hello nello stesso dominio padre può essere ospitato in hello stessa distribuzione di gateway applicazione. Tra gli esempi dell'uso di sottodomini si possono includere http://blog.contoso.com e http://app.contoso.com ospitati in una singola distribuzione del gateway applicazione.

## <a name="host-headers-and-server-name-indication-sni"></a>Intestazioni host e indicazione nome server (SNI)

Esistono tre meccanismi comuni per l'abilitazione del sito più hosting in hello stessa infrastruttura.

1. Ospitare più applicazioni Web con un indirizzo IP univoco per ognuna.
2. Nome di host di usare toohost più applicazioni web su hello stesso indirizzo IP.
3. Usa diversa porte toohost più applicazioni web su hello stesso indirizzo IP.

Un gateway applicazione ottiene attualmente un singolo indirizzo IP pubblico su cui rimane in ascolto del traffico. Di conseguenza, non è attualmente possibile supportare più applicazioni ognuna con il proprio indirizzo IP. Gateway applicazione supporta più applicazioni di hosting ogni in ascolto su porte diverse, ma questo scenario richiede il traffico di hello applicazioni tooaccept sulle porte non standard e spesso non è una configurazione desiderata. Gateway applicazione si basa su HTTP 1.1 toohost intestazioni host più di un sito Web in hello stesso indirizzo IP pubblico e la porta. siti Hello ospitati su gateway applicazione possono inoltre il supporto di offload SSL con l'estensione di indicazione nome Server (SNI) TLS. Questo scenario significa che Hello client browser e back-end web farm devono supportare HTTP/1.1 ed estensione TLS come definito in RFC 6066.

## <a name="listener-configuration-element"></a>Elemento di configurazione del listener

HTTPListener esistente è di elemento di configurazione avanzata toosupport host nome e il server indica gli elementi name, che viene utilizzato dal pool di applicazioni gateway tooroute traffico tooappropriate back-end. Hello esempio di codice seguente è hello frammento dell'elemento di listener HTTP dal file di modello.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

È possibile visitare [modello Resource Manager utilizza l'hosting del sito più](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) per una distribuzione di fine tooend basato su modello.

## <a name="routing-rule"></a>Regola di routing

Non è richiesta nella regola di routing hello alcuna modifica. Hello toobe scelto tootie hello sito appropriato listener toohello corrispondente back-end pool di indirizzi deve continuare 'Basic' regola di routing.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Passaggi successivi

Dopo avere learning sull'hosting di più siti, andare troppo[creare un gateway applicazione utilizza l'hosting del sito più](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate un gateway applicazione con capacità toosupport più di una sola applicazione web.

