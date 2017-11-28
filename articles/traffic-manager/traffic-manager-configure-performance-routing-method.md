---
title: metodo di routing tramite Azure Traffic Manager il traffico prestazioni aaaConfigure | Documenti Microsoft
description: "Questo articolo viene illustrato come tooconfigure tooroute Traffic Manager il traffico toohello endpoint con latenza più bassa"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="d32dc-103">Configurare il metodo di routing del traffico delle prestazioni di hello</span><span class="sxs-lookup"><span data-stu-id="d32dc-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="d32dc-104">Hello metodo di routing del traffico di prestazioni consente di toodirect traffico toohello endpoint con latenza più bassa di hello dalla rete hello del client.</span><span class="sxs-lookup"><span data-stu-id="d32dc-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="d32dc-105">In genere, hello Data Center con latenza più bassa hello è hello più vicino nella distanza geografica.</span><span class="sxs-lookup"><span data-stu-id="d32dc-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="d32dc-106">Questo metodo di routing del traffico non può basarsi per le modifiche in tempo reale sul carico o sulla configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="d32dc-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="d32dc-107">metodo di routing prestazioni tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d32dc-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="d32dc-108">Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d32dc-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d32dc-109">Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d32dc-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="d32dc-110">Nella barra di ricerca del portale hello, cercare hello **profili di gestione traffico** e quindi fare clic su nome del profilo hello desiderati come metodo di routing hello tooconfigure per.</span><span class="sxs-lookup"><span data-stu-id="d32dc-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="d32dc-111">In hello **profilo di gestione traffico** pannello, verificare che sia hello servizi cloud e siti Web che si desidera tooinclude nella configurazione sono presenti.</span><span class="sxs-lookup"><span data-stu-id="d32dc-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="d32dc-112">In hello **impostazioni** fare clic su **configurazione**e in hello **configurazione** pannello completo come segue:</span><span class="sxs-lookup"><span data-stu-id="d32dc-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="d32dc-113">Nelle **impostazioni del metodo di routing del traffico** per **Metodo di routing** selezionare **Prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="d32dc-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="d32dc-114">Set hello **le impostazioni di monitoraggio Endpoint** identici per tutti i ogni endpoint in questo profilo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d32dc-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="d32dc-115">Seleziona hello appropriato **protocollo**e specificare hello **porta** numero.</span><span class="sxs-lookup"><span data-stu-id="d32dc-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="d32dc-116">In **Percorso** immettere una barra */*.</span><span class="sxs-lookup"><span data-stu-id="d32dc-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="d32dc-117">toomonitor endpoint, è necessario specificare un percorso e nome file.</span><span class="sxs-lookup"><span data-stu-id="d32dc-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="d32dc-118">Barra "/" è una voce valida per il percorso relativo hello e implica che il file hello trovi nella directory radice di hello (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="d32dc-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="d32dc-119">Nella parte superiore di hello della pagina hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d32dc-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="d32dc-120">Testare le modifiche di hello nella configurazione, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d32dc-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="d32dc-121">Nella barra di ricerca del portale hello, cercare il nome del profilo di Traffic Manager hello e scegliere il profilo di gestione traffico hello nei risultati di hello che hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d32dc-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="d32dc-122">In hello **Traffic Manager** profilo pannello, fare clic su **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="d32dc-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="d32dc-123">Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato.</span><span class="sxs-lookup"><span data-stu-id="d32dc-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="d32dc-124">È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello.</span><span class="sxs-lookup"><span data-stu-id="d32dc-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="d32dc-125">In questo caso tutte le richieste vengono indirizzato toohello endpoint con latenza più bassa di hello dalla rete hello del client.</span><span class="sxs-lookup"><span data-stu-id="d32dc-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="d32dc-126">Dopo avere utilizza profilo di Traffic Manager, modificare il record DNS hello nel toopoint di server DNS autorevole il nome di dominio della società dominio nome toohello Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d32dc-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Configurazione del metodo di routing del traffico delle prestazioni con Gestione traffico][1]

## <a name="next-steps"></a><span data-ttu-id="d32dc-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d32dc-128">Next steps</span></span>

- <span data-ttu-id="d32dc-129">Informazioni sul [metodo di routing del traffico Ponderato](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d32dc-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="d32dc-130">Informazioni sul [metodo di routing Priorità](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d32dc-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="d32dc-131">Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d32dc-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="d32dc-132">Informazioni su come troppo[verificare le impostazioni di gestione traffico](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d32dc-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png