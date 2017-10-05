---
title: Supporto HTTP/2 nella rete CDN di Azure| Microsoft Docs
description: Informazioni sul supporto HTTP/2 e la rete CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="d5a79-103">Supporto HTTP/2 nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d5a79-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d5a79-104">HTTP/2 è una revisione principale HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="d5a79-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="d5a79-105">Fornisce più velocemente esperienza utente migliorata, tempo di risposta ridotto e delle prestazioni web, mantenendo i metodi HTTP familiarità, codici di stato e semantica.</span><span class="sxs-lookup"><span data-stu-id="d5a79-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="d5a79-106">Anche se HTTP/2 è progettato per funzionare con HTTP e HTTPS, molti browser Web client supportano solo HTTP/2 su TLS.</span><span class="sxs-lookup"><span data-stu-id="d5a79-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="d5a79-107">Vantaggi di HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d5a79-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="d5a79-108">I vantaggi di HTTP/2 includono:</span><span class="sxs-lookup"><span data-stu-id="d5a79-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="d5a79-109">**Multiplexing e concorrenza**</span><span class="sxs-lookup"><span data-stu-id="d5a79-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="d5a79-110">Usando HTTP 1.1, se si eseguono più richieste di risorse multiple sono necessarie più connessioni TCP e a ogni connessione è associato un overhead delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d5a79-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="d5a79-111">HTTP/2 consente di richiedere più risorse in un'unica connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="d5a79-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="d5a79-112">**Compressione delle intestazioni**</span><span class="sxs-lookup"><span data-stu-id="d5a79-112">**Header compression**</span></span>

    <span data-ttu-id="d5a79-113">Comprimendo le intestazioni HTTP per le risorse servite, il tempo di trasferimento è ridotto in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="d5a79-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="d5a79-114">**Dipendenze del flusso**</span><span class="sxs-lookup"><span data-stu-id="d5a79-114">**Stream dependencies**</span></span>

    <span data-ttu-id="d5a79-115">Le dipendenze del flusso consentono al client di indicare al server le risorse con priorità.</span><span class="sxs-lookup"><span data-stu-id="d5a79-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="d5a79-116">Supporto browser HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d5a79-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="d5a79-117">Tutti i browser principali hanno implementato il supporto HTTP/2 le versioni correnti.</span><span class="sxs-lookup"><span data-stu-id="d5a79-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="d5a79-118">Per i browser non supportati ci sarà il fallback automatico a HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="d5a79-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="d5a79-119">Browser</span><span class="sxs-lookup"><span data-stu-id="d5a79-119">Browser</span></span>|<span data-ttu-id="d5a79-120">Versione minima</span><span class="sxs-lookup"><span data-stu-id="d5a79-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="d5a79-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d5a79-121">Microsoft Edge</span></span>| <span data-ttu-id="d5a79-122">12</span><span class="sxs-lookup"><span data-stu-id="d5a79-122">12</span></span>|
|<span data-ttu-id="d5a79-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d5a79-123">Google Chrome</span></span>| <span data-ttu-id="d5a79-124">43</span><span class="sxs-lookup"><span data-stu-id="d5a79-124">43</span></span>|
|<span data-ttu-id="d5a79-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d5a79-125">Mozilla Firefox</span></span>| <span data-ttu-id="d5a79-126">38</span><span class="sxs-lookup"><span data-stu-id="d5a79-126">38</span></span>|
|<span data-ttu-id="d5a79-127">Opera</span><span class="sxs-lookup"><span data-stu-id="d5a79-127">Opera</span></span>| <span data-ttu-id="d5a79-128">32</span><span class="sxs-lookup"><span data-stu-id="d5a79-128">32</span></span>|
|<span data-ttu-id="d5a79-129">Safari</span><span class="sxs-lookup"><span data-stu-id="d5a79-129">Safari</span></span>| <span data-ttu-id="d5a79-130">9</span><span class="sxs-lookup"><span data-stu-id="d5a79-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="d5a79-131">Abilitazione del supporto HTTP/2 nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d5a79-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d5a79-132">Attualmente il supporto HTTP/2 è attivo per i profili di **rete CDN di Azure di Akamai** e di **rete CDN di Azure di Verizon**.</span><span class="sxs-lookup"><span data-stu-id="d5a79-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="d5a79-133">Non è necessaria alcuna azione da parte dei clienti.</span><span class="sxs-lookup"><span data-stu-id="d5a79-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="d5a79-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5a79-134">Next Steps</span></span>

<span data-ttu-id="d5a79-135">Per visualizzare i vantaggi di HTTP/2 in azione, vedere [questa demo di Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="d5a79-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="d5a79-136">Per altre informazioni su HTTP/2, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5a79-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="d5a79-137">Home page delle specifiche HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d5a79-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="d5a79-138">Domande frequenti su HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d5a79-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="d5a79-139">Informazioni su HTTP/2 di Akamai</span><span class="sxs-lookup"><span data-stu-id="d5a79-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="d5a79-140">Per altre informazioni sulle funzionalità disponibili della rete CDN di Azure, vedere [Panoramica della rete CDN di Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="d5a79-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>