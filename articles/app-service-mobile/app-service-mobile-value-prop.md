---
title: Informazioni su App per dispositivi mobili nel servizio app di Azure
description: "Informazioni sui vantaggi che il servizio app può apportare alle app per dispositivi mobili aziendali."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="ec98e-103"><a name="getting-started"> </a>Informazioni su App per dispositivi mobili nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ec98e-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="ec98e-104">Il servizio app di Azure è un'offerta di [piattaforma distribuita come servizio ](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) interamente gestita per sviluppatori professionisti.</span><span class="sxs-lookup"><span data-stu-id="ec98e-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="ec98e-105">Il servizio offre un set completo di funzionalità per scenari Web, per dispositivi mobili e di integrazione.</span><span class="sxs-lookup"><span data-stu-id="ec98e-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="ec98e-106">La funzionalità App per dispositivi mobili del servizio app di Azure offre a integratori di sistemi e sviluppatori aziendali una piattaforma di sviluppo di applicazioni per dispositivi mobili con scalabilità elevata e disponibilità globale.</span><span class="sxs-lookup"><span data-stu-id="ec98e-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Panoramica visiva delle funzionalità di App per dispositivi mobili](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="ec98e-108">Perché le app per dispositivi mobili?</span><span class="sxs-lookup"><span data-stu-id="ec98e-108">Why Mobile Apps?</span></span>
<span data-ttu-id="ec98e-109">Con la funzionalità App per dispositivi mobili, è possibile:</span><span class="sxs-lookup"><span data-stu-id="ec98e-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="ec98e-110">**Compilare app native e multipiattaforma**. Sia che si compilino app native iOS, Android e Windows o app multipiattaforma Xamarin o Cordova (PhoneGap), è possibile sfruttare il servizio app usando SDK nativi.</span><span class="sxs-lookup"><span data-stu-id="ec98e-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="ec98e-111">**Connettersi ai sistemi aziendali**. Con la funzionalità App per dispositivi mobili, è possibile aggiungere l'accesso aziendale in pochi minuti e connettersi alle risorse aziendali locali o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="ec98e-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="ec98e-112">**Compilare app offline con sincronizzazione dei dati**. È possibile aumentare la produttività della forza lavoro mobile compilando app eseguibili offline e usando App per dispositivi mobili per sincronizzare i dati in background quando è disponibile la connettività con qualsiasi origine dati o API SaaS (Software as a Service) aziendale.</span><span class="sxs-lookup"><span data-stu-id="ec98e-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="ec98e-113">**Inviare notifiche push a milioni di utenti in pochi secondi**. È possibile coinvolgere i clienti con notifiche push immediate su qualsiasi dispositivo, personalizzate in base alle specifiche esigenze e inviate al momento giusto.</span><span class="sxs-lookup"><span data-stu-id="ec98e-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="ec98e-114">Funzionalità di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="ec98e-114">Mobile Apps features</span></span>
<span data-ttu-id="ec98e-115">Le funzionalità seguenti sono importanti per lo sviluppo per dispositivi mobili abilitati per il cloud:</span><span class="sxs-lookup"><span data-stu-id="ec98e-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="ec98e-116">**Autenticazione e autorizzazione**. È possibile scegliere da un elenco in costante crescita di provider di identità, tra cui Azure Active Directory per l'autenticazione aziendale, nonché provider di servizi di social networking come Facebook, Google, Twitter e account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ec98e-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="ec98e-117">App per dispositivi mobili offre un servizio OAuth 2.0 per ogni provider.</span><span class="sxs-lookup"><span data-stu-id="ec98e-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="ec98e-118">È anche possibile integrare l'SDK del provider di identità per funzionalità specifiche del provider.</span><span class="sxs-lookup"><span data-stu-id="ec98e-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="ec98e-119">Altre informazioni sulle [funzionalità di autenticazione].</span><span class="sxs-lookup"><span data-stu-id="ec98e-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="ec98e-120">**Accesso ai dati**. App per dispositivi mobili offre un'origine dati OData v3 ottimizzata per dispositivi mobili collegata al database SQL di Azure o a un'istanza locale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ec98e-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="ec98e-121">Dato che questo servizio può essere basato su Entity Framework, consente una facile integrazione con altri provider di dati NoSQL e SQL, tra cui [Archiviazione tabelle di Azure], MongoDB e [Azure Cosmos DB], e provider di API SaaS come Office 365 e Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="ec98e-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="ec98e-122">**Sincronizzazione offline**. Gli SDK client facilitano la compilazione di applicazioni per dispositivi mobili solide e reattive che funzionano con un set di dati offline.</span><span class="sxs-lookup"><span data-stu-id="ec98e-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="ec98e-123">Il set di dati può essere sincronizzato con i dati back-end, con supporto della risoluzione dei conflitti.</span><span class="sxs-lookup"><span data-stu-id="ec98e-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="ec98e-124">Altre informazioni sulle [funzionalità dati].</span><span class="sxs-lookup"><span data-stu-id="ec98e-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="ec98e-125">**Notifiche push**. Gli SDK client si integrano facilmente con le funzionalità di registrazione di Hub di notifica di Azure, consentendo di inviare notifiche push a milioni di utenti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ec98e-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="ec98e-126">Altre informazioni sulle [funzionalità di notifica push].</span><span class="sxs-lookup"><span data-stu-id="ec98e-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="ec98e-127">**SDK client**. Viene offerto un set completo di SDK client che coprono lo sviluppo nativo ([iOS], [Android] e [Windows]), multipiattaforma ([Xamarin.iOS, Xamarin.Android] e [Xamarin.Forms]) e di applicazioni ibride ([Apache Cordova]).</span><span class="sxs-lookup"><span data-stu-id="ec98e-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="ec98e-128">Ogni SDK client è disponibile con una licenza MIT ed è open source.</span><span class="sxs-lookup"><span data-stu-id="ec98e-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="ec98e-129">Funzionalità del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ec98e-129">Azure App Service features</span></span>
<span data-ttu-id="ec98e-130">Le funzionalità della piattaforma seguenti sono utili per i siti di produzione per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="ec98e-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="ec98e-131">**Scalabilità automatica**. Il servizio app consente di aumentare rapidamente le prestazioni o il numero di istanze per gestire qualsiasi carico di lavoro in ingresso dei clienti.</span><span class="sxs-lookup"><span data-stu-id="ec98e-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="ec98e-132">È possibile selezionare manualmente il numero e le dimensioni delle VM o configurare la scalabilità automatica per ridimensionare il back-end delle app per dispositivi mobili in base al carico o alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="ec98e-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="ec98e-133">Altre informazioni sulla [scalabilità automatica].</span><span class="sxs-lookup"><span data-stu-id="ec98e-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="ec98e-134">**Ambienti di staging**. Il servizio app può eseguire più versioni del sito e consente così di eseguire test A/B, test in ambiente di produzione nell'ambito di un piano DevOps più ampio e staging sul posto di un nuovo back-end.</span><span class="sxs-lookup"><span data-stu-id="ec98e-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="ec98e-135">Altre informazioni sugli [ambienti di staging].</span><span class="sxs-lookup"><span data-stu-id="ec98e-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="ec98e-136">**Distribuzione continua**. Il servizio app può integrarsi con i comuni sistemi di gestione della supply chain e consente così di distribuire automaticamente una nuova versione del back-end eseguendo il push in un ramo del sistema di gestione della supply chain.</span><span class="sxs-lookup"><span data-stu-id="ec98e-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="ec98e-137">Altre informazioni sulle [opzioni di distribuzione].</span><span class="sxs-lookup"><span data-stu-id="ec98e-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="ec98e-138">**Rete virtuale**. Il servizio app può connettersi alle risorse locali usando una rete virtuale, Azure ExpressRoute o connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="ec98e-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="ec98e-139">Altre informazioni su [connessioni ibride], [reti virtuali] ed [ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="ec98e-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="ec98e-140">**Ambienti isolati e dedicati**. È possibile eseguire il servizio app in un ambiente completamente isolato e dedicato per l'esecuzione sicura delle app del servizio app di Azure su larga scala.</span><span class="sxs-lookup"><span data-stu-id="ec98e-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="ec98e-141">Un ambiente di questo tipo è ideale per i carichi di lavoro delle applicazioni che richiedono scalabilità elevata, isolamento o accesso alla rete sicuro.</span><span class="sxs-lookup"><span data-stu-id="ec98e-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="ec98e-142">Altre informazioni sugli [ambienti del servizio app].</span><span class="sxs-lookup"><span data-stu-id="ec98e-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec98e-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ec98e-143">Next steps</span></span>

<span data-ttu-id="ec98e-144">Per iniziare a usare App per dispositivi mobili nel servizio app di Azure, completare l'[esercitazione introduttiva].</span><span class="sxs-lookup"><span data-stu-id="ec98e-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="ec98e-145">L'esercitazione illustra le nozioni di base della creazione di un back-end e un client per dispositivi mobili di propria scelta,</span><span class="sxs-lookup"><span data-stu-id="ec98e-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="ec98e-146">nonché l'integrazione dell'autenticazione, della sincronizzazione offline e delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="ec98e-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="ec98e-147">È possibile completare l'esercitazione più volte, una per ogni applicazione client.</span><span class="sxs-lookup"><span data-stu-id="ec98e-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="ec98e-148">Per altre informazioni su App per dispositivi mobili, vedere la [mappa di apprendimento].</span><span class="sxs-lookup"><span data-stu-id="ec98e-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="ec98e-149">Per altre informazioni sulla piattaforma del servizio app di Azure, vedere [Servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="ec98e-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Servizio app di Azure]: ../app-service/app-service-value-prop-what-is.md
[esercitazione introduttiva]: app-service-mobile-ios-get-started.md
[Archiviazione tabelle di Azure]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[funzionalità di autenticazione]: ./app-service-mobile-auth.md
[funzionalità dati]: ./app-service-mobile-offline-data-sync.md
[funzionalità di notifica push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS, Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[scalabilità automatica]: ../app-service-web/web-sites-scale.md
[ambienti di staging]: ../app-service-web/web-sites-staged-publishing.md
[opzioni di distribuzione]: ../app-service-web/web-sites-deploy.md
[connessioni ibride]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[reti virtuali]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[ambienti del servizio app]: ../app-service-web/app-service-app-service-environment-intro.md
[mappa di apprendimento]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
