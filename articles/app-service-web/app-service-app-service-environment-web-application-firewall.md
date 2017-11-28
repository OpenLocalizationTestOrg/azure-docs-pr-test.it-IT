---
title: Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app
description: Informazioni su come configurare un Web application firewall davanti all'ambiente del servizio app.
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="e70ab-103">Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="e70ab-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="e70ab-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e70ab-104">Overview</span></span>
<span data-ttu-id="e70ab-105">[Barracuda WAF per Azure](https://www.barracuda.com/programs/azure) è un web application firewall disponibile in [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) che consente di proteggere le applicazioni Web esaminando il traffico Web in ingresso per bloccare SQL injection, attacchi tramite script da altri siti, caricamenti di malware, DDoS di applicazioni e altri attacchi.</span><span class="sxs-lookup"><span data-stu-id="e70ab-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="e70ab-106">Esamina anche le risposte provenienti dai server Web back-end per la prevenzione della perdita dei dati.</span><span class="sxs-lookup"><span data-stu-id="e70ab-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="e70ab-107">In associazione all'isolamento e alla scalabilità aggiuntiva fornita dagli ambienti del servizio app, costituisce un ambiente ideale per le applicazioni Web critiche per l'azienda, che devono sostenere richieste dannose e un volume elevato di traffico.</span><span class="sxs-lookup"><span data-stu-id="e70ab-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="e70ab-108">Configurazione</span><span class="sxs-lookup"><span data-stu-id="e70ab-108">Setup</span></span>
<span data-ttu-id="e70ab-109">Per questo documento si configurerà l'ambiente del servizio app dietro più istanze con carico bilanciato di Barracuda WAF, in modo che solo il traffico proveniente dal firewall WAF possa raggiungere l'ambiente del servizio app che non sarà accessibile dalla rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="e70ab-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="e70ab-110">Gestione traffico di Azure sarà invece davanti alle istanze di Barracuda WAF per bilanciare il carico tra i data center e le aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="e70ab-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="e70ab-111">Il diagramma generale della configurazione sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e70ab-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="e70ab-113">Nota: con l'introduzione del [supporto del bilanciamento del carico interno per l'ambiente del servizio app](app-service-environment-with-internal-load-balancer.md), è possibile configurare l'ambiente del servizio app in modo che risulti inaccessibile dalla rete perimetrale e sia disponibile solo per la rete privata.</span><span class="sxs-lookup"><span data-stu-id="e70ab-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="e70ab-114">Configurazione dell'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="e70ab-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="e70ab-115">Per configurare un ambiente del servizio app, fare riferimento alla [documentazione](app-service-web-how-to-create-an-app-service-environment.md) sull'argomento.</span><span class="sxs-lookup"><span data-stu-id="e70ab-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="e70ab-116">Al termine della creazione di un ambiente del servizio app, è possibile creare in questo ambiente le [app Web](app-service-web-overview.md), le [app per le API](../app-service-api/app-service-api-apps-why-best-platform.md) e le [app per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md) che saranno protette dietro il firewall WAF che verrà configurato nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="e70ab-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="e70ab-117">Configurazione del servizio Cloud Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="e70ab-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="e70ab-118">Sul sito Barracuda è disponibile un [articolo dettagliato](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sulla distribuzione del firewall WAF in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="e70ab-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="e70ab-119">Poiché tuttavia quello che si vuole è la ridondanza senza introdurre un singolo punto di guasto, è opportuno distribuire almeno 2 VM con istanze WAF nello stesso servizio cloud quando si seguono queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e70ab-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="e70ab-120">Aggiunta di endpoint al servizio cloud</span><span class="sxs-lookup"><span data-stu-id="e70ab-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="e70ab-121">Una volta create 2 o più istanze di macchine virtuali WAF nel servizio cloud, è possibile usare il [portale di Azure](https://portal.azure.com/) per aggiungere endpoint HTTP e HTTPS usati dall'applicazione, come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="e70ab-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Configurare l'endpoint][ConfigureEndpoint]

<span data-ttu-id="e70ab-123">Se le applicazioni usano altri endpoint, assicurarsi di aggiungerli tutti a questo elenco.</span><span class="sxs-lookup"><span data-stu-id="e70ab-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="e70ab-124">Configurazione di Barracuda WAF tramite il relativo portale di gestione</span><span class="sxs-lookup"><span data-stu-id="e70ab-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="e70ab-125">Barracuda WAF usa la porta TCP 8000 per la configurazione tramite il proprio portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="e70ab-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="e70ab-126">Poiché ci sono più istanze di VM WAF, sarà necessario ripetere questi passaggi per ogni istanza di VM.</span><span class="sxs-lookup"><span data-stu-id="e70ab-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="e70ab-127">Nota: una volta completata la configurazione WAF, rimuovere l'endpoint TCP/8000 da tutte le VM WAF per mantenere protetto il firewall WAF.</span><span class="sxs-lookup"><span data-stu-id="e70ab-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="e70ab-128">Aggiungere l'endpoint di gestione, come illustrato nell'immagine seguente, per configurare Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="e70ab-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Aggiungere l'endpoint di gestione][AddManagementEndpoint]

<span data-ttu-id="e70ab-130">Usare un browser per passare all'endpoint di gestione nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e70ab-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="e70ab-131">Se il servizio cloud si chiama test.cloudapp.net, si accederà a questo endpoint passando a http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="e70ab-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="e70ab-132">Dovrebbe essere visualizzata una pagina di accesso come quella seguente a cui è possibile accedere usando le credenziali specificate in fase di configurazione delle VM WAF.</span><span class="sxs-lookup"><span data-stu-id="e70ab-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Pagina di accesso gestione][ManagementLoginPage]

<span data-ttu-id="e70ab-134">Dopo l'accesso, dovrebbe essere visualizzato un dashboard come quello nell'immagine seguente che presenterà le statistiche di base sulla protezione WAF.</span><span class="sxs-lookup"><span data-stu-id="e70ab-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Dashboard di gestione][ManagementDashboard]

<span data-ttu-id="e70ab-136">Fare clic sulla scheda Services per configurare il firewall WAF per i servizi protetti.</span><span class="sxs-lookup"><span data-stu-id="e70ab-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="e70ab-137">Per altri dettagli sulla configurazione di Barracuda WAF, è possibile consultare la [relativa documentazione](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="e70ab-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="e70ab-138">Nell'esempio seguente, è stata configurata un'app Web di Azure che gestisce il traffico su HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e70ab-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Aggiunta di servizi di gestione][ManagementAddServices]

> <span data-ttu-id="e70ab-140">Nota: a seconda di come sono configurate le applicazioni e di quali funzionalità sono in uso nell'ambiente del servizio app, sarà necessario inoltrare il traffico per le porte TCP diverse dalla 80 e dalla 443, ad esempio se IP SSL è configurato per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="e70ab-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="e70ab-141">Per un elenco di porte di rete usate negli ambienti del servizio app, fare riferimento alla sezione Porte di rete della [documentazione sul controllo del traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) .</span><span class="sxs-lookup"><span data-stu-id="e70ab-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="e70ab-142">Configurazione di Gestione traffico di Microsoft Azure (FACOLTATIVO)</span><span class="sxs-lookup"><span data-stu-id="e70ab-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="e70ab-143">Se l'applicazione è disponibile in più aree, è preferibile bilanciarne il carico dietro [Gestione traffico di Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e70ab-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="e70ab-144">A questo scopo, è possibile aggiungere un endpoint nel [portale di Azure classico](https://manage.azure.com) usando il nome del servizio cloud per WAF nel profilo di Gestione traffico come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="e70ab-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Endpoint di Gestione traffico][TrafficManagerEndpoint]

<span data-ttu-id="e70ab-146">Se l'applicazione richiede l'autenticazione, assicurarsi di disporre di qualche risorsa che non richiede alcuna autenticazione per consentire a Gestione traffico di effettuare il ping per la disponibilità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e70ab-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="e70ab-147">È possibile configurare l'URL nella sezione Configura del [portale di Azure classico](https://manage.azure.com) come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e70ab-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configurare Gestione traffico][ConfigureTrafficManager]

<span data-ttu-id="e70ab-149">Per inoltrare i ping di Gestione traffico dal firewall WAF all'applicazione, è necessario configurare Website Translations in Barracuda WAF per inoltrare il traffico all'applicazione, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e70ab-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="e70ab-151">Protezione del traffico verso l'ambiente del servizio app con i gruppi di sicurezza di rete (NSG)</span><span class="sxs-lookup"><span data-stu-id="e70ab-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="e70ab-152">Attenersi alla [documentazione sul controllo del traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) per informazioni dettagliate sulla limitazione del traffico all'ambiente del servizio app dal firewall WAF usando solo l'indirizzo VIP del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e70ab-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="e70ab-153">Ecco un comando di Powershell di esempio per eseguire questa attività per la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="e70ab-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="e70ab-154">Sostituire SourceAddressPrefix con l'indirizzo IP virtuale (VIP) del servizio cloud del firewall WAF.</span><span class="sxs-lookup"><span data-stu-id="e70ab-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="e70ab-155">Nota: l'indirizzo VIP del servizio cloud cambia quando si elimina e si ricrea il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e70ab-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="e70ab-156">In questo caso, assicurarsi di aggiornare l'indirizzo IP nel gruppo di risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="e70ab-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
