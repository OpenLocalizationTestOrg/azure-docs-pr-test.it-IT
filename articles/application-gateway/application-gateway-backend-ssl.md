---
title: aaaEnabling fine tooend SSL nel Gateway di applicazione di Azure | Documenti Microsoft
description: Questa pagina viene fornita una panoramica di hello Gateway applicazione end tooend supporto SSL.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a><span data-ttu-id="5e305-103">Panoramica di fine tooend SSL con Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="5e305-103">Overview of end tooend SSL with Application Gateway</span></span>

<span data-ttu-id="5e305-104">Gateway applicazione supporta la terminazione SSL gateway hello, dopo che il traffico passa in genere non crittografati toohello i server back-end.</span><span class="sxs-lookup"><span data-stu-id="5e305-104">Application gateway supports SSL termination at hello gateway, after which traffic typically flows unencrypted toohello backend servers.</span></span> <span data-ttu-id="5e305-105">Questa funzionalità consente di web server toobe unburdened da sovraccarico di crittografia e decrittografia costoso.</span><span class="sxs-lookup"><span data-stu-id="5e305-105">This feature allows web servers toobe unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="5e305-106">Per alcuni clienti server back-end toohello di comunicazione non crittografata non è tuttavia un'opzione accettabile.</span><span class="sxs-lookup"><span data-stu-id="5e305-106">However for some customers unencrypted communication toohello backend servers is not an acceptable option.</span></span> <span data-ttu-id="5e305-107">Questa comunicazione non crittografata potrebbe essere dovuto toosecurity requisiti, i requisiti di conformità, o un'applicazione hello può accettare solo una connessione sicura.</span><span class="sxs-lookup"><span data-stu-id="5e305-107">This unencrypted communication could be due toosecurity requirements, compliance requirements, or hello application may only accept a secure connection.</span></span> <span data-ttu-id="5e305-108">Per tali applicazioni, i gateway applicazione supporta fine tooend SSL crittografia.</span><span class="sxs-lookup"><span data-stu-id="5e305-108">For such applications, application gateway supports end tooend SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="5e305-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5e305-109">Overview</span></span>

<span data-ttu-id="5e305-110">Fine tooend SSL consente toosecurely trasmettere back-end toohello dati sensibili crittografati mentre vengono comunque usufruire dei vantaggi di hello della funzionalità di bilanciamento del carico di livello 7 il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="5e305-110">End tooend SSL allows you toosecurely transmit sensitive data toohello backend encrypted while still taking advantage of hello benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="5e305-111">Alcune di queste funzionalità sono l'affinità di sessione basato su cookie, il routing basato su URL, il supporto per il routing basato su siti o possibilità tooinject - inoltrati - X * intestazioni.</span><span class="sxs-lookup"><span data-stu-id="5e305-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability tooinject X-Forwarded-* headers.</span></span>

<span data-ttu-id="5e305-112">Quando è configurato con la modalità di comunicazione end tooend SSL, gateway applicazione termina le sessioni SSL hello gateway hello e decrittografa il traffico utente.</span><span class="sxs-lookup"><span data-stu-id="5e305-112">When configured with end tooend SSL communication mode, application gateway terminates hello SSL sessions at hello gateway and decrypts user traffic.</span></span> <span data-ttu-id="5e305-113">Viene quindi applicata hello configurata regole tooselect un back-end appropriata pool istanza tooroute del traffico.</span><span class="sxs-lookup"><span data-stu-id="5e305-113">It then applies hello configured rules tooselect an appropriate backend pool instance tooroute traffic to.</span></span> <span data-ttu-id="5e305-114">Gateway applicazione quindi avvia un nuovo server di back-end toohello connessione SSL e crittografare nuovamente i dati tramite certificato di chiave pubblica del server back-end hello prima della trasmissione hello back-end toohello di richiesta.</span><span class="sxs-lookup"><span data-stu-id="5e305-114">Application gateway then initiates a new SSL connection toohello backend server and re-encrypts data using hello backend server's public key certificate before transmitting hello request toohello backend.</span></span> <span data-ttu-id="5e305-115">Fine tooend che SSL è abilitato impostando l'impostazione del protocollo in tooHTTPS BackendHTTPSetting, che viene quindi applicato pool back-end tooa.</span><span class="sxs-lookup"><span data-stu-id="5e305-115">End tooend SSL is enabled by setting protocol setting in BackendHTTPSetting tooHTTPS, which is then applied tooa backend pool.</span></span> <span data-ttu-id="5e305-116">Ogni server di back-end nel pool back-end di hello con SSL abilitato tooend di fine deve essere configurato con una comunicazione protetta tooallow di certificato.</span><span class="sxs-lookup"><span data-stu-id="5e305-116">Each backend server in hello backend pool with end tooend SSL enabled must be configured with a certificate tooallow secure communication.</span></span>

![scenario di end tooend ssl][1]

<span data-ttu-id="5e305-118">In questo esempio, le richieste tramite TLS 1.2 sono server toobackend indirizzato Pool1 utilizzando tooend fine SSL.</span><span class="sxs-lookup"><span data-stu-id="5e305-118">In this example, requests using TLS1.2 are routed toobackend servers in Pool1 using end tooend SSL.</span></span>

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="5e305-119">Terminare tooend SSL e whitelist dei certificati</span><span class="sxs-lookup"><span data-stu-id="5e305-119">End tooend SSL and whitelisting of certificates</span></span>

<span data-ttu-id="5e305-120">Gateway applicazione comunica solo con le istanze di back-end noto che hanno consentito il proprio certificato al gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e305-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with hello application gateway.</span></span> <span data-ttu-id="5e305-121">whitelist tooenable dei certificati, è necessario caricare la chiave pubblica hello di gateway applicazione back-end server certificati toohello (non certificato radice hello).</span><span class="sxs-lookup"><span data-stu-id="5e305-121">tooenable whitelisting of certificates, you must upload hello public key of backend server certificates toohello application gateway (not hello root certificate).</span></span> <span data-ttu-id="5e305-122">Solo le connessioni tooknown e consentito back-end sono quindi consentiti.</span><span class="sxs-lookup"><span data-stu-id="5e305-122">Only connections tooknown and whitelisted backends are then allowed.</span></span> <span data-ttu-id="5e305-123">Hello rimanenti back-end genera un errore di gateway.</span><span class="sxs-lookup"><span data-stu-id="5e305-123">hello remaining backends results in a gateway error.</span></span> <span data-ttu-id="5e305-124">I certificati autofirmati vengono usati a scopo di test e non sono consigliati per i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5e305-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="5e305-125">Tali certificati hanno consentito di toobe con il gateway applicazione hello come descritto in hello passaggi precedenti, prima di poter essere usati.</span><span class="sxs-lookup"><span data-stu-id="5e305-125">Such certificates have toobe whitelisted with hello application gateway as described in hello preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e305-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e305-126">Next steps</span></span>

<span data-ttu-id="5e305-127">Dopo avere imparare a fine tooend SSL, andare troppo[abilitare fine tooend SSL nel gateway applicazione](application-gateway-end-to-end-ssl-powershell.md) toocreate gateway un'applicazione che utilizza end tooend SSL.</span><span class="sxs-lookup"><span data-stu-id="5e305-127">After learning about end tooend SSL, go too[enable end tooend SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) toocreate an application gateway using end tooend SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
