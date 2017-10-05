---
title: File Leggimi dell'ambiente del servizio app di Azure
description: Elenca la documentazione che descrive l'ambiente del servizio app di Azure
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 5b1362854dbc3b0098718bd2ea3cffb06366000c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="e236c-103">Documentazione relativa all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="e236c-103">App Service environment documentation</span></span>
 <span data-ttu-id="e236c-104">Ambiente del servizio app di Azure è una funzionalità del servizio app di Azure che fornisce un ambiente completamente isolato e dedicato per l'esecuzione sicura di app del servizio app di Azure su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="e236c-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="e236c-105">Questa funzionalità può ospitare [app Web][webapps], [app per dispositivi mobili][mobileapps], [app per le API][APIApps] e [Funzioni][Functions].</span><span class="sxs-lookup"><span data-stu-id="e236c-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="e236c-106">Gli ambienti del servizio app sono ideali per i carichi di lavoro dell'applicazione che richiedono:</span><span class="sxs-lookup"><span data-stu-id="e236c-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="e236c-107">Scalabilità molto elevata.</span><span class="sxs-lookup"><span data-stu-id="e236c-107">Very high scale.</span></span>
* <span data-ttu-id="e236c-108">Isolamento e accesso alla rete protetto.</span><span class="sxs-lookup"><span data-stu-id="e236c-108">Isolation and secure network access.</span></span>

<span data-ttu-id="e236c-109">I clienti possono creare più ambienti del servizio app sia in una singola area di Azure che in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="e236c-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="e236c-110">Questa versatilità rende gli ambienti del servizio app ideali per i livelli applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro RPS elevati.</span><span class="sxs-lookup"><span data-stu-id="e236c-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="e236c-111">Gli ambienti del servizio app sono isolati per eseguire solo le applicazioni di un singolo cliente e sono sempre distribuiti in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e236c-111">ASEs are isolated to running only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="e236c-112">I clienti hanno il controllo con granularità fine del traffico di rete in ingresso e in uscita dell'applicazione tramite [gruppi di sicurezza di rete][NSGs].</span><span class="sxs-lookup"><span data-stu-id="e236c-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="e236c-113">Le applicazioni possono anche stabilire connessioni protette ad alta velocità su reti virtuali con risorse aziendali locali.</span><span class="sxs-lookup"><span data-stu-id="e236c-113">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="e236c-114">Spesso le app devono accedere a risorse aziendali, ad esempio database e servizi Web interni.</span><span class="sxs-lookup"><span data-stu-id="e236c-114">Apps frequently need to access corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="e236c-115">Le app in esecuzione in ambienti del servizio app possono accedere alle risorse tramite VPN [da sito a sito][SiteToSite] e connessioni [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="e236c-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="e236c-116">[Che cos'è un ambiente del servizio app?][Intro]</span><span class="sxs-lookup"><span data-stu-id="e236c-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="e236c-117">[Creare un ambiente del servizio app][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="e236c-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="e236c-118">[Creare un ambiente del servizio app con bilanciamento del carico interno][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="e236c-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="e236c-119">[Usare un ambiente del servizio app][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="e236c-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="e236c-120">[Considerazioni sulla rete e ambiente del servizio app][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="e236c-120">[Networking considerations and the App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="e236c-121">[Creare un ambiente del servizio app da un modello][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="e236c-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="e236c-122">Video</span><span class="sxs-lookup"><span data-stu-id="e236c-122">Videos</span></span>
<span data-ttu-id="e236c-123">Master Modern PaaS for the Enterprise with Azure App Service (Gestire una PaaS aziendale moderna con il Servizio app di Azure)</span><span class="sxs-lookup"><span data-stu-id="e236c-123">Master Modern PaaS for the Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="e236c-124">Deploying Highly Scalable and Secure Apps (Distribuzione di app altamente scalabili e sicure)</span><span class="sxs-lookup"><span data-stu-id="e236c-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="e236c-125">Running Enterprise Web and Mobile Apps on Azure App Service (Esecuzione di app aziendali Web e per dispositivi mobili nel Servizio app di Azure)</span><span class="sxs-lookup"><span data-stu-id="e236c-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="e236c-126">Ambiente del servizio app 1</span><span class="sxs-lookup"><span data-stu-id="e236c-126">App Service Environment v1</span></span> ##
<span data-ttu-id="e236c-127">Esistono due versioni dell'ambiente del servizio app: ASEv1 e ASEv2.</span><span class="sxs-lookup"><span data-stu-id="e236c-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="e236c-128">Per informazioni sulla versione ASEv1, vedere [Documentazione relativa agli ambienti del servizio app][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="e236c-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
