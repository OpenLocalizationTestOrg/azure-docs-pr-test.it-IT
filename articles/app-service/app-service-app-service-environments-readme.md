---
title: Ambiente del servizio aaaApp | Documenti Microsoft
description: "Che cos'è un ambiente del servizio app di Azure? Un'introduzione tooApp ambiente del servizio."
keywords: ambiente del servizio app di azure, rete virtuale, rete protetta
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="a0b23-105">Documentazione relativa agli ambienti del servizio app</span><span class="sxs-lookup"><span data-stu-id="a0b23-105">App Service Environment Documentation</span></span>
<span data-ttu-id="a0b23-106">Un ambiente di servizio app è un'opzione del piano di servizio [Premium][PremiumTier] di Servizio app di Azure che fornisce un ambiente completamente isolato e dedicato all'esecuzione sicura delle app di Servizio di Azure su larga scala, tra cui [app Web][WebApps], [app per dispositivi mobili][MobileApps], e [app per le API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="a0b23-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="a0b23-107">Gli ambienti di servizi di app sono ideali per i carichi di lavoro dell'applicazione che richiedono:</span><span class="sxs-lookup"><span data-stu-id="a0b23-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="a0b23-108">Scalabilità molto elevata</span><span class="sxs-lookup"><span data-stu-id="a0b23-108">Very high scale</span></span>
* <span data-ttu-id="a0b23-109">Isolamento e accesso alla rete protetto</span><span class="sxs-lookup"><span data-stu-id="a0b23-109">Isolation and secure network access</span></span>

<span data-ttu-id="a0b23-110">I clienti possono creare più ambienti di servizi di applicazione in una singola area di Azure, nonché in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0b23-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="a0b23-111">Questo rende gli Ambienti di servizio dell’App ideali per i livelli dell’applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro elevati RPS.</span><span class="sxs-lookup"><span data-stu-id="a0b23-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="a0b23-112">Gli ambienti del servizio App sono isolati toorunning solo le applicazioni di un singolo cliente e vengono sempre distribuiti in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a0b23-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="a0b23-113">I clienti hanno il controllo con granularità fine del traffico di rete in ingresso e in uscita dell'applicazione tramite [gruppi di sicurezza di rete][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="a0b23-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="a0b23-114">Le applicazioni inoltre possono stabilire connessioni protette ad alta velocità sulle risorse di reti virtuali tooon tra più sedi aziendali.</span><span class="sxs-lookup"><span data-stu-id="a0b23-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="a0b23-115">App è spesso necessitano tooaccess alle risorse aziendali, ad esempio servizi web e database interni.</span><span class="sxs-lookup"><span data-stu-id="a0b23-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="a0b23-116">Le applicazioni in esecuzione in ambienti del servizio app possono accedere alle risorse raggiungibili tramite connessioni VPN [da sito a sito][SiteToSite] e [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="a0b23-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="a0b23-117">Che cos'è un ambiente del servizio app?</span><span class="sxs-lookup"><span data-stu-id="a0b23-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="a0b23-118">Creazione di un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a0b23-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="a0b23-119">Creazione di app in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a0b23-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="a0b23-120">Creazione e uso di un servizio di bilanciamento del carico interno con ambienti del servizio App</span><span class="sxs-lookup"><span data-stu-id="a0b23-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="a0b23-121">Configurazione di un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a0b23-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="a0b23-122">Scalabilità di app in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a0b23-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="a0b23-123">Sicurezza di rete e architettura</span><span class="sxs-lookup"><span data-stu-id="a0b23-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="a0b23-124">Procedure</span><span class="sxs-lookup"><span data-stu-id="a0b23-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="a0b23-125">Video</span><span class="sxs-lookup"><span data-stu-id="a0b23-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
