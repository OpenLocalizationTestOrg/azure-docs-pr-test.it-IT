---
title: supporto aaaHTTP/2 nella rete CDN di Azure | Documenti Microsoft
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="d15c0-103">Supporto HTTP/2 nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d15c0-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d15c0-104">HTTP/2 è tooHTTP/1.1\ una revisione principale.</span><span class="sxs-lookup"><span data-stu-id="d15c0-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="d15c0-105">Fornisce più velocemente esperienza utente migliorata, tempo di risposta ridotto e delle prestazioni web, mantenendo i metodi HTTP familiarità hello, codici di stato e semantica.</span><span class="sxs-lookup"><span data-stu-id="d15c0-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="d15c0-106">HTTP/2, anche se toowork progettato con HTTP e HTTPS, molti browser web client supportano solo HTTP/2 tramite TLS.</span><span class="sxs-lookup"><span data-stu-id="d15c0-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="d15c0-107">Vantaggi di HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d15c0-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="d15c0-108">Hello HTTP/2 seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d15c0-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="d15c0-109">**Multiplexing e concorrenza**</span><span class="sxs-lookup"><span data-stu-id="d15c0-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="d15c0-110">Usando HTTP 1.1, se si eseguono più richieste di risorse multiple sono necessarie più connessioni TCP e a ogni connessione è associato un overhead delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d15c0-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="d15c0-111">HTTP/2 consente più toobe risorse richiesto in una singola connessione TCP.</span><span class="sxs-lookup"><span data-stu-id="d15c0-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="d15c0-112">**Compressione delle intestazioni**</span><span class="sxs-lookup"><span data-stu-id="d15c0-112">**Header compression**</span></span>

    <span data-ttu-id="d15c0-113">Comprimendo le intestazioni HTTP hello per le risorse fornite, tempo durante la trasmissione hello viene ridotto in modo significativo.</span><span class="sxs-lookup"><span data-stu-id="d15c0-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="d15c0-114">**Dipendenze del flusso**</span><span class="sxs-lookup"><span data-stu-id="d15c0-114">**Stream dependencies**</span></span>

    <span data-ttu-id="d15c0-115">Dipendenze di flusso consentono ai client hello tooindicate toohello server quali risorse hanno la priorità.</span><span class="sxs-lookup"><span data-stu-id="d15c0-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="d15c0-116">Supporto browser HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d15c0-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="d15c0-117">Tutti i browser principali hello stato implementato il supporto HTTP/2 le versioni correnti.</span><span class="sxs-lookup"><span data-stu-id="d15c0-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="d15c0-118">Browser non supportati verranno automaticamente il fallback tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="d15c0-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="d15c0-119">Browser</span><span class="sxs-lookup"><span data-stu-id="d15c0-119">Browser</span></span>|<span data-ttu-id="d15c0-120">Versione minima</span><span class="sxs-lookup"><span data-stu-id="d15c0-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="d15c0-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="d15c0-121">Microsoft Edge</span></span>| <span data-ttu-id="d15c0-122">12</span><span class="sxs-lookup"><span data-stu-id="d15c0-122">12</span></span>|
|<span data-ttu-id="d15c0-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="d15c0-123">Google Chrome</span></span>| <span data-ttu-id="d15c0-124">43</span><span class="sxs-lookup"><span data-stu-id="d15c0-124">43</span></span>|
|<span data-ttu-id="d15c0-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="d15c0-125">Mozilla Firefox</span></span>| <span data-ttu-id="d15c0-126">38</span><span class="sxs-lookup"><span data-stu-id="d15c0-126">38</span></span>|
|<span data-ttu-id="d15c0-127">Opera</span><span class="sxs-lookup"><span data-stu-id="d15c0-127">Opera</span></span>| <span data-ttu-id="d15c0-128">32</span><span class="sxs-lookup"><span data-stu-id="d15c0-128">32</span></span>|
|<span data-ttu-id="d15c0-129">Safari</span><span class="sxs-lookup"><span data-stu-id="d15c0-129">Safari</span></span>| <span data-ttu-id="d15c0-130">9</span><span class="sxs-lookup"><span data-stu-id="d15c0-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="d15c0-131">Abilitazione del supporto HTTP/2 nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d15c0-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="d15c0-132">Attualmente il supporto HTTP/2 è attivo per i profili di **rete CDN di Azure di Akamai** e di **rete CDN di Azure di Verizon**.</span><span class="sxs-lookup"><span data-stu-id="d15c0-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="d15c0-133">Non è necessaria alcuna azione da parte dei clienti.</span><span class="sxs-lookup"><span data-stu-id="d15c0-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="d15c0-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d15c0-134">Next Steps</span></span>

<span data-ttu-id="d15c0-135">vantaggi di hello toosee HTTP/2 in azione, vedere [questa demo da Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="d15c0-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="d15c0-136">toolearn ulteriori informazioni su HTTP/2, visitare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d15c0-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="d15c0-137">Home page delle specifiche HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d15c0-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="d15c0-138">Domande frequenti su HTTP/2</span><span class="sxs-lookup"><span data-stu-id="d15c0-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="d15c0-139">Informazioni su HTTP/2 di Akamai</span><span class="sxs-lookup"><span data-stu-id="d15c0-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="d15c0-140">toolearn sulle funzionalità disponibili della rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="d15c0-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
