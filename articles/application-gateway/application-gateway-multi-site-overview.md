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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="82a20-103">Hosting di più siti in un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="82a20-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="82a20-104">Hosting di più siti consente tooconfigure più di una sola applicazione web su hello stessa istanza di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="82a20-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="82a20-105">Questa funzionalità permette di tooconfigure una topologia più efficiente per le distribuzioni tramite l'aggiunta di gateway applicazione tooone di too20 siti Web.</span><span class="sxs-lookup"><span data-stu-id="82a20-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="82a20-106">Ogni sito Web può essere indirizzato tooits proprietari pool back-end.</span><span class="sxs-lookup"><span data-stu-id="82a20-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="82a20-107">Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com da due pool di server back-end denominato ContosoServerPool e FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="82a20-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="82a20-109">Le regole vengono elaborate in ordine di hello che sono elencati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="82a20-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="82a20-110">È tooconfiguring precedente prima tooconfigure consigliata multisito listener un listener di base.</span><span class="sxs-lookup"><span data-stu-id="82a20-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="82a20-111">In questo modo di terminare tale traffico Ottiene indirizzato toohello nuovo.</span><span class="sxs-lookup"><span data-stu-id="82a20-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="82a20-112">Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.</span><span class="sxs-lookup"><span data-stu-id="82a20-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="82a20-113">Le richieste per http://contoso.com tooContosoServerPool indirizzato e http://fabrikam.com tooFabrikamServerPool indirizzato.</span><span class="sxs-lookup"><span data-stu-id="82a20-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="82a20-114">Analogamente, due sottodomini di hello nello stesso dominio padre può essere ospitato in hello stessa distribuzione di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="82a20-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="82a20-115">Tra gli esempi dell'uso di sottodomini si possono includere http://blog.contoso.com e http://app.contoso.com ospitati in una singola distribuzione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="82a20-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="82a20-116">Intestazioni host e indicazione nome server (SNI)</span><span class="sxs-lookup"><span data-stu-id="82a20-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="82a20-117">Esistono tre meccanismi comuni per l'abilitazione del sito più hosting in hello stessa infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="82a20-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="82a20-118">Ospitare più applicazioni Web con un indirizzo IP univoco per ognuna.</span><span class="sxs-lookup"><span data-stu-id="82a20-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="82a20-119">Nome di host di usare toohost più applicazioni web su hello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="82a20-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="82a20-120">Usa diversa porte toohost più applicazioni web su hello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="82a20-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="82a20-121">Un gateway applicazione ottiene attualmente un singolo indirizzo IP pubblico su cui rimane in ascolto del traffico.</span><span class="sxs-lookup"><span data-stu-id="82a20-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="82a20-122">Di conseguenza, non è attualmente possibile supportare più applicazioni ognuna con il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="82a20-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="82a20-123">Gateway applicazione supporta più applicazioni di hosting ogni in ascolto su porte diverse, ma questo scenario richiede il traffico di hello applicazioni tooaccept sulle porte non standard e spesso non è una configurazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="82a20-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="82a20-124">Gateway applicazione si basa su HTTP 1.1 toohost intestazioni host più di un sito Web in hello stesso indirizzo IP pubblico e la porta.</span><span class="sxs-lookup"><span data-stu-id="82a20-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="82a20-125">siti Hello ospitati su gateway applicazione possono inoltre il supporto di offload SSL con l'estensione di indicazione nome Server (SNI) TLS.</span><span class="sxs-lookup"><span data-stu-id="82a20-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="82a20-126">Questo scenario significa che Hello client browser e back-end web farm devono supportare HTTP/1.1 ed estensione TLS come definito in RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="82a20-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="82a20-127">Elemento di configurazione del listener</span><span class="sxs-lookup"><span data-stu-id="82a20-127">Listener configuration element</span></span>

<span data-ttu-id="82a20-128">HTTPListener esistente è di elemento di configurazione avanzata toosupport host nome e il server indica gli elementi name, che viene utilizzato dal pool di applicazioni gateway tooroute traffico tooappropriate back-end.</span><span class="sxs-lookup"><span data-stu-id="82a20-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="82a20-129">Hello esempio di codice seguente è hello frammento dell'elemento di listener HTTP dal file di modello.</span><span class="sxs-lookup"><span data-stu-id="82a20-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="82a20-130">È possibile visitare [modello Resource Manager utilizza l'hosting del sito più](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) per una distribuzione di fine tooend basato su modello.</span><span class="sxs-lookup"><span data-stu-id="82a20-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="82a20-131">Regola di routing</span><span class="sxs-lookup"><span data-stu-id="82a20-131">Routing rule</span></span>

<span data-ttu-id="82a20-132">Non è richiesta nella regola di routing hello alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="82a20-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="82a20-133">Hello toobe scelto tootie hello sito appropriato listener toohello corrispondente back-end pool di indirizzi deve continuare 'Basic' regola di routing.</span><span class="sxs-lookup"><span data-stu-id="82a20-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82a20-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82a20-134">Next steps</span></span>

<span data-ttu-id="82a20-135">Dopo avere learning sull'hosting di più siti, andare troppo[creare un gateway applicazione utilizza l'hosting del sito più](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate un gateway applicazione con capacità toosupport più di una sola applicazione web.</span><span class="sxs-lookup"><span data-stu-id="82a20-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

