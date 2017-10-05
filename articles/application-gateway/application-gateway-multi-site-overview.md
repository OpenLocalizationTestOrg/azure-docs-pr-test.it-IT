---
title: "Hosting di più siti in un gateway applicazione di Azure | Microsoft Docs"
description: "Questa pagina offre una panoramica del supporto di più siti in un gateway applicazione."
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
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="2c217-103">Hosting di più siti in un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="2c217-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="2c217-104">L'hosting di più siti consente di configurare più applicazioni Web nella stessa istanza del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c217-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="2c217-105">Questa funzionalità consente di configurare una topologia più efficiente per le distribuzioni aggiungendo fino a 20 siti Web a un unico gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c217-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="2c217-106">Ogni sito Web può essere indirizzato al proprio pool back-end.</span><span class="sxs-lookup"><span data-stu-id="2c217-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="2c217-107">Nell'esempio seguente, il gateway applicazione gestisce il traffico per contoso.com e fabrikam.com da due pool di server back-end denominati ContosoServerPool e FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="2c217-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="2c217-109">Le regole vengono elaborate nell'ordine in cui sono elencate nel portale.</span><span class="sxs-lookup"><span data-stu-id="2c217-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="2c217-110">È consigliabile configurare i listener multisito prima di configurare un listener di base.</span><span class="sxs-lookup"><span data-stu-id="2c217-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="2c217-111">In questo modo il traffico viene indirizzato al back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="2c217-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="2c217-112">Se un listener di base viene elencato per primo e corrisponde a una richiesta in ingresso, sarà tale listener a elaborarla.</span><span class="sxs-lookup"><span data-stu-id="2c217-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="2c217-113">Le richieste per http://contoso.com vengono instradate a ContosoServerPool, mentre quelle per http://fabrikam.com vengono instradate a FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="2c217-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="2c217-114">Analogamente, la stessa distribuzione del gateway applicazione può ospitare due sottodomini dello stesso dominio padre.</span><span class="sxs-lookup"><span data-stu-id="2c217-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="2c217-115">Tra gli esempi dell'uso di sottodomini si possono includere http://blog.contoso.com e http://app.contoso.com ospitati in una singola distribuzione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c217-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="2c217-116">Intestazioni host e indicazione nome server (SNI)</span><span class="sxs-lookup"><span data-stu-id="2c217-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="2c217-117">Per abilitare l'hosting di più siti nella stessa infrastruttura sono disponibili tre comuni meccanismi.</span><span class="sxs-lookup"><span data-stu-id="2c217-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="2c217-118">Ospitare più applicazioni Web con un indirizzo IP univoco per ognuna.</span><span class="sxs-lookup"><span data-stu-id="2c217-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="2c217-119">Usare il nome host per ospitare più applicazioni Web nello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2c217-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="2c217-120">Usare porte diverse per ospitare più applicazioni Web nello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2c217-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="2c217-121">Un gateway applicazione ottiene attualmente un singolo indirizzo IP pubblico su cui rimane in ascolto del traffico.</span><span class="sxs-lookup"><span data-stu-id="2c217-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="2c217-122">Di conseguenza, non è attualmente possibile supportare più applicazioni ognuna con il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2c217-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="2c217-123">Il gateway applicazione supporta l'hosting di più applicazioni ognuna in ascolto su porte diverse, ma in questo scenario le applicazioni dovrebbero accettare traffico su porte non standard e questa non è in genere una configurazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="2c217-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="2c217-124">Il gateway applicazione si basa su intestazioni host HTTP 1.1 per ospitare più siti Web nello stesso indirizzo IP pubblico e nella stessa porta.</span><span class="sxs-lookup"><span data-stu-id="2c217-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="2c217-125">I siti ospitati nel gateway applicazione possono supportare anche l'offload SSL con l'estensione TLS dell'indicazione nome server (SNI).</span><span class="sxs-lookup"><span data-stu-id="2c217-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="2c217-126">In questo scenario il browser client e la Web farm back-end devono quindi supportare HTTP/1.1 e l'estensione TLS definita nella specifica RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="2c217-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="2c217-127">Elemento di configurazione del listener</span><span class="sxs-lookup"><span data-stu-id="2c217-127">Listener configuration element</span></span>

<span data-ttu-id="2c217-128">L'elemento di configurazione HTTPListener esistente è stato migliorato per supportare gli elementi del nome host e dell'indicazione nome server usati dal gateway applicazione per instradare il traffico al pool back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="2c217-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="2c217-129">L'esempio di codice seguente è il frammento dell'elemento HttpListeners del file modello.</span><span class="sxs-lookup"><span data-stu-id="2c217-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="2c217-130">Per una distribuzione basata su modello end-to-end, vedere il [modello di Resource Manager con hosting di più siti](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting).</span><span class="sxs-lookup"><span data-stu-id="2c217-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="2c217-131">Regola di routing</span><span class="sxs-lookup"><span data-stu-id="2c217-131">Routing rule</span></span>

<span data-ttu-id="2c217-132">Nella regola di routing non è necessaria alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="2c217-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="2c217-133">È ancora necessario scegliere la regola di routing "Basic" per collegare il listener del sito appropriato al pool di indirizzi back-end corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2c217-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2c217-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c217-134">Next steps</span></span>

<span data-ttu-id="2c217-135">Dopo aver acquisito familiarità con l'hosting di più siti, vedere [Creare un gateway applicazione per l'hosting di più applicazioni Web](application-gateway-create-multisite-azureresourcemanager-powershell.md) per creare un gateway applicazione con supporto di più applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="2c217-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

