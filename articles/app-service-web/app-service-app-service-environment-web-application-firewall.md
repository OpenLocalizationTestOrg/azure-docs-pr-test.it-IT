---
title: aaaConfiguring un Firewall applicazione Web (WAF) per l'ambiente del servizio App
description: Informazioni su come un'applicazione web tooconfigure firewall davanti l'ambiente del servizio App.
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
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="06403-103">Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="06403-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="06403-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="06403-104">Overview</span></span>
<span data-ttu-id="06403-105">Firewall applicazione come hello Web [WAF Barracuda per Azure](https://www.barracuda.com/programs/azure) disponibile su hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) consente di proteggere le applicazioni web controllando tooblock traffico web in ingresso SQL attacchi injection, Cross-Site Scripting, caricamenti di malware & applicazione DDoS e altri attacchi.</span><span class="sxs-lookup"><span data-stu-id="06403-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="06403-106">Inoltre analizza le risposte hello dai server back-end web hello per la prevenzione della perdita di dati (DLP).</span><span class="sxs-lookup"><span data-stu-id="06403-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="06403-107">In combinazione con l'isolamento di hello e scalabilità aggiuntive fornite per gli ambienti del servizio App, ciò offre un ambiente ideale toohost aziendali critici applicazioni che richiedono le richieste dannose toowithstand e traffico elevato.</span><span class="sxs-lookup"><span data-stu-id="06403-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="06403-108">Configurazione</span><span class="sxs-lookup"><span data-stu-id="06403-108">Setup</span></span>
<span data-ttu-id="06403-109">Per questo documento che verrà configurato l'ambiente del servizio App dietro più carico bilanciato le istanze di WAF Barracuda in modo che solo il traffico da WAF hello può raggiungere hello ambiente del servizio App e non sarà accessibile dalla rete Perimetrale hello.</span><span class="sxs-lookup"><span data-stu-id="06403-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="06403-110">Si disporrà di Traffic Manager di Azure davanti il saldo di tooload Barracuda WAF istanze tra data center di Azure e le aree.</span><span class="sxs-lookup"><span data-stu-id="06403-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="06403-111">Un diagramma di alto livello del programma di installazione di hello avrà un aspetto simile a quello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="06403-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Architettura][Architecture] 

> <span data-ttu-id="06403-113">Nota: con introduzione hello di [ILB supporto per l'ambiente del servizio App](app-service-environment-with-internal-load-balancer.md), è possibile configurare toobe hello ASE accessibile dalla rete Perimetrale hello ed essere solo la rete privata toohello disponibili.</span><span class="sxs-lookup"><span data-stu-id="06403-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="06403-114">Configurazione dell'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="06403-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="06403-115">un ambiente del servizio App tooconfigure vedere troppo[documentazione](app-service-web-how-to-create-an-app-service-environment.md) oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="06403-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="06403-116">Dopo aver creato un ambiente del servizio App, è possibile creare [App Web](app-service-web-overview.md), [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md) e [App per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md) in questo ambiente che sarà possibile proteggere dietro WAF hello è configurare la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="06403-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="06403-117">Configurazione del servizio Cloud Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="06403-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="06403-118">Sul sito Barracuda è disponibile un [articolo dettagliato](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sulla distribuzione del firewall WAF in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="06403-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="06403-119">Ma poiché si desidera la ridondanza e non introduce un singolo punto di errore, si desidera che toodeploy almeno 2 WAF istanza macchine virtuali in hello nello stesso servizio Cloud quando queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="06403-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="06403-120">Aggiunta di tooCloud endpoint servizio</span><span class="sxs-lookup"><span data-stu-id="06403-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="06403-121">Dopo aver 2 o VM WAF altre istanze nel servizio Cloud, è possibile utilizzare hello [portale di Azure](https://portal.azure.com/) tooadd endpoint HTTP e HTTPS utilizzate dall'applicazione, come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="06403-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Configurare l'endpoint][ConfigureEndpoint]

<span data-ttu-id="06403-123">Se le applicazioni utilizzano altri endpoint, assicurarsi anche tali elenco toothis tooadd che.</span><span class="sxs-lookup"><span data-stu-id="06403-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="06403-124">Configurazione di Barracuda WAF tramite il relativo portale di gestione</span><span class="sxs-lookup"><span data-stu-id="06403-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="06403-125">Barracuda WAF usa la porta TCP 8000 per la configurazione tramite il proprio portale di gestione.</span><span class="sxs-lookup"><span data-stu-id="06403-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="06403-126">Poiché vi sono più istanze di macchine virtuali WAF hello occorre toorepeat hello questa procedura per ogni istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06403-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="06403-127">Nota: Termine con configurazione WAF, rimuovere endpoint TCP/8000 hello da tutti i tookeep di macchine virtuali WAF il WAF sicura.</span><span class="sxs-lookup"><span data-stu-id="06403-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="06403-128">Aggiungere hello Gestione endpoint come illustrato nell'immagine di hello sotto tooconfigure WAF il dispositivo Barracuda.</span><span class="sxs-lookup"><span data-stu-id="06403-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Aggiungere l'endpoint di gestione][AddManagementEndpoint]

<span data-ttu-id="06403-130">Utilizzare un endpoint di gestione toohello toobrowse browser sul servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="06403-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="06403-131">Se il servizio Cloud viene chiamato test.cloudapp.net, è necessario accedere a questo endpoint esplorando toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="06403-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="06403-132">Si noterà una pagina di accesso come il seguente che è possibile accedere utilizzando le credenziali specificate in fase di installazione di hello WAF VM.</span><span class="sxs-lookup"><span data-stu-id="06403-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Pagina di accesso gestione][ManagementLoginPage]

<span data-ttu-id="06403-134">Una volta accesso si dovrebbe essere visualizzato un dashboard come hello uno nell'immagine di hello seguito presenterà le statistiche di base sulla protezione WAF hello.</span><span class="sxs-lookup"><span data-stu-id="06403-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Dashboard di gestione][ManagementDashboard]

<span data-ttu-id="06403-136">Facendo clic sulla scheda Servizi hello consente di configurare il WAF per i servizi che protegge.</span><span class="sxs-lookup"><span data-stu-id="06403-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="06403-137">Per altri dettagli sulla configurazione di Barracuda WAF, è possibile consultare la [relativa documentazione](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="06403-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="06403-138">Nell'esempio hello sotto un'App Web di Azure gestisce il traffico su HTTP e HTTPS è stata configurata.</span><span class="sxs-lookup"><span data-stu-id="06403-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Aggiunta di servizi di gestione][ManagementAddServices]

> <span data-ttu-id="06403-140">Nota: A seconda di come vengono configurate le applicazioni e le funzionalità sono usate nell'ambiente del servizio App, sarà necessario tooforward traffico per le porte TCP diverso da 80 e 443, ad esempio, se il programma di installazione di IP SSL per un'App Web.</span><span class="sxs-lookup"><span data-stu-id="06403-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="06403-141">Per un elenco delle porte di rete utilizzata in ambienti di servizio App, fare riferimento troppo[documentazione di controllare il traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) sezione porte di rete.</span><span class="sxs-lookup"><span data-stu-id="06403-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="06403-142">Configurazione di Gestione traffico di Microsoft Azure (FACOLTATIVO)</span><span class="sxs-lookup"><span data-stu-id="06403-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="06403-143">Se l'applicazione è disponibile in più aree, quindi è opportuno bilanciare tooload loro dietro [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="06403-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="06403-144">toodo è quindi possibile aggiungere un endpoint in hello [portale di Azure classico](https://manage.azure.com) utilizzando nome del servizio Cloud hello per le WAF nel profilo di Traffic Manager hello, come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="06403-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Endpoint di Gestione traffico][TrafficManagerEndpoint]

<span data-ttu-id="06403-146">Se l'applicazione richiede l'autenticazione, assicurarsi di che disporre di alcune risorse che non richiedono alcuna autenticazione per tooping gestione traffico per la disponibilità dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="06403-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="06403-147">È possibile configurare l'URL di hello nella sezione Configurazione hello in hello [portale di Azure classico](https://manage.azure.com) come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="06403-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configurare Gestione traffico][ConfigureTrafficManager]

<span data-ttu-id="06403-149">ping di Traffic Manager tooforward hello dall'applicazione tooyour WAF, è necessario traduzioni del sito Web toosetup sull'applicazione Barracuda WAF tooforward traffico tooyour come illustrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="06403-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="06403-151">Proteggere il traffico tooApp servizio ambiente con sicurezza gruppi (rete)</span><span class="sxs-lookup"><span data-stu-id="06403-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="06403-152">Seguire hello [documentazione di controllare il traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) per ulteriori informazioni sulla limitazione del traffico tooyour ambiente del servizio App da hello WAF solo utilizzando l'indirizzo VIP hello del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="06403-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="06403-153">Ecco un comando di Powershell di esempio per eseguire questa attività per la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="06403-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="06403-154">Sostituire hello SourceAddressPrefix con indirizzo di IP virtuale (VIP) del servizio Cloud del WAF hello.</span><span class="sxs-lookup"><span data-stu-id="06403-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="06403-155">Nota: hello VIP del servizio Cloud verrà modificato se si elimina e ricrea hello servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="06403-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="06403-156">Verificare che tooupdate hello indirizzo nel gruppo di risorse di rete hello dopo l'installazione.</span><span class="sxs-lookup"><span data-stu-id="06403-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
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
