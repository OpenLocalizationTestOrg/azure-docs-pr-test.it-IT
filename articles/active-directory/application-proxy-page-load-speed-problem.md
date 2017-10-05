---
title: Il caricamento dell'applicazione del proxy di applicazione impiega troppo tempo | Microsoft Docs
description: Risoluzione dei problemi delle prestazioni di caricamento della pagina con il proxy di applicazione di Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="56e84-103">Il caricamento dell'applicazione del proxy di applicazione impiega troppo tempo</span><span class="sxs-lookup"><span data-stu-id="56e84-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="56e84-104">Questo articolo aiuta a comprendere perché il caricamento di un'applicazione del proxy di applicazione di Azure AD potrebbe impiegare troppo tempo e illustra cosa è possibile fare per risolvere tale problema.</span><span class="sxs-lookup"><span data-stu-id="56e84-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="56e84-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="56e84-105">Overview</span></span>
<span data-ttu-id="56e84-106">Se le applicazioni funzionano ma si riscontra una lunga latenza, per migliorare la velocità potrebbero essere prese in considerazione piccole modifiche da applicare alla topologia di rete.</span><span class="sxs-lookup"><span data-stu-id="56e84-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="56e84-107">Per una valutazione delle diverse topologie, consultare il [documento relativo alle considerazioni sulla rete](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="56e84-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="56e84-108">Se queste considerazioni non sono utili, purtroppo al momento non abbiamo altri consigli per ottimizzare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="56e84-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="56e84-109">Quando il servizio proxy di applicazione si espande a più data center in prossimità dell'utente, potrebbe essere possibile iniziare a vedere direttamente un miglioramento della latenza.</span><span class="sxs-lookup"><span data-stu-id="56e84-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="56e84-110">Per un l'elenco completo dei data center di Azure, è possibile visualizzare la [pagina di prova della latenza](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="56e84-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="56e84-111">I data center con il servizio proxy di applicazione sono disponibili con lo [strumento per il test delle porte del connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="56e84-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="56e84-112">Commenti sulle posizioni dei data center del proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="56e84-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="56e84-113">Potrebbero essere presenti data center di Azure che non includono ancora il proxy di applicazione e, di conseguenza, potrebbero migliorare di tanto la latenza.</span><span class="sxs-lookup"><span data-stu-id="56e84-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="56e84-114">È possibile inviare un feedback sulla posizione dei data center all'indirizzo <aadapfeedback@microsoft.com>, che potremo utilizzare per i futuri piani di espansione.</span><span class="sxs-lookup"><span data-stu-id="56e84-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="56e84-115">Stiamo inoltre lavorando per aggiungere funzionalità in grado di migliorare la latenza per i tenant che attualmente riscontrano tempi di latenza troppo lunghi. Condivideremo tutta la documentazione non appena disponibile.</span><span class="sxs-lookup"><span data-stu-id="56e84-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56e84-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56e84-116">Next steps</span></span>
[<span data-ttu-id="56e84-117">Usare server proxy locali esistenti</span><span class="sxs-lookup"><span data-stu-id="56e84-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
