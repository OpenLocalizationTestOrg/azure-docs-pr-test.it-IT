---
title: Abilitazione di SSL end-to-end nel gateway applicazione di Azure | Microsoft Docs
description: Questa pagina offre un'introduzione al supporto di SSL end-to-end del gateway applicazione.
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
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="1da33-103">Panoramica di SSL end-to-end con il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="1da33-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="1da33-104">Il gateway applicazione supporta la terminazione SSL nel gateway, dopo la quale il traffico scorre generalmente non crittografato verso i server back-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="1da33-105">Questa funzionalità consente ai server Web di non gestire il costoso carico di crittografia e decrittografia.</span><span class="sxs-lookup"><span data-stu-id="1da33-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="1da33-106">Tuttavia, per alcuni clienti le comunicazioni non crittografate verso i server back-end non rappresentano un'opzione accettabile.</span><span class="sxs-lookup"><span data-stu-id="1da33-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="1da33-107">Le comunicazioni non crittografate potrebbero essere causate da requisiti di sicurezza o conformità oppure da un'applicazione che può accettare solo una connessione protetta.</span><span class="sxs-lookup"><span data-stu-id="1da33-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="1da33-108">Per tali applicazioni, il gateway applicazione supporta ora la crittografia SSL end-to-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="1da33-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1da33-109">Overview</span></span>

<span data-ttu-id="1da33-110">La crittografia SSL end-to-end consente di trasmettere in modo sicuro dati sensibili crittografati al back-end, usufruendo comunque dei vantaggi delle funzionalità di bilanciamento del carico di livello 7 offerte dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1da33-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="1da33-111">Alcune di queste funzionalità sono l'affinità di sessione basata su cookie, il routing basato su URL, il supporto per il routing basato su siti o la possibilità di inserire intestazioni X-Forwarded-*.</span><span class="sxs-lookup"><span data-stu-id="1da33-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="1da33-112">Se configurato con la modalità di comunicazione SSL end-to-end, il gateway applicazione termina le sessioni SSL nel gateway ed esegue la decrittografia del traffico utente.</span><span class="sxs-lookup"><span data-stu-id="1da33-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="1da33-113">Applica quindi le regole configurate per selezionare un'istanza del pool di back-end adeguata su cui instradare il traffico.</span><span class="sxs-lookup"><span data-stu-id="1da33-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="1da33-114">Il gateway applicazione avvia a questo punto una nuova connessione SSL al server back-end e crittografa nuovamente i dati usando il certificato di chiave pubblica del server back-end prima di trasmettere la richiesta al back-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="1da33-115">Per abilitare SSL end-to-end si imposta la configurazione del protocollo in BackendHTTPSetting su HTTPS. Questa impostazione viene quindi applicata a un pool back-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="1da33-116">Per una comunicazione protetta, ogni server back-end nel pool di back-end con SSL end-to-end abilitato deve essere configurato con un certificato.</span><span class="sxs-lookup"><span data-stu-id="1da33-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![Scenario di SSL end-to-end][1]

<span data-ttu-id="1da33-118">In questo esempio, le richieste che usano TLS1.2 vengono instradate ai server back-end in Pool1 con SSL end-to-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="1da33-119">SSL end-to-end e aggiunta dei certificati all'elenco dei consentiti</span><span class="sxs-lookup"><span data-stu-id="1da33-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="1da33-120">Il gateway applicazione comunica solo con istanze back-end note, il cui certificato è incluso nell'elenco dei consentiti del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="1da33-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="1da33-121">Per abilitare l'aggiunta dei certificati all'elenco dei consentiti, è necessario caricare nel gateway applicazione la chiave pubblica dei certificati dei server back-end (non il certificato radice).</span><span class="sxs-lookup"><span data-stu-id="1da33-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="1da33-122">Sono quindi consentite solo le connessioni a back-end noti e inclusi nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="1da33-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="1da33-123">Gli altri back-end generano un errore del gateway.</span><span class="sxs-lookup"><span data-stu-id="1da33-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="1da33-124">I certificati autofirmati vengono usati a scopo di test e non sono consigliati per i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1da33-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="1da33-125">Prima dell'uso, anche questi certificati devono essere aggiunti all'elenco dei consentiti nel gateway applicazione, come descritto nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="1da33-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1da33-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1da33-126">Next steps</span></span>

<span data-ttu-id="1da33-127">Dopo avere appreso i concetti di SSL end-to-end, passare all'articolo che spiega come [abilitare SSL end-to-end nel gateway applicazione](application-gateway-end-to-end-ssl-powershell.md) per creare un gateway applicazione usando SSL end-to-end.</span><span class="sxs-lookup"><span data-stu-id="1da33-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
