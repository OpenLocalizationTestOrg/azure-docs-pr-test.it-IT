---
title: applicazione Proxy di applicazione aaaAn accetta tooload troppo lungo | Documenti Microsoft
description: Risolvere i problemi di prestazioni di caricamento pagina con hello Proxy dell'applicazione Azure Active
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="56aad-103">Un'applicazione di Proxy applicazione impiega troppo tempo tooload</span><span class="sxs-lookup"><span data-stu-id="56aad-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="56aad-104">Questo articolo è utile toounderstand perché un'applicazione Proxy dell'applicazione Azure Active Directory potrebbe richiedere un tooload molto tempo e cosa è possibile eseguire tooresolve questo problema.</span><span class="sxs-lookup"><span data-stu-id="56aad-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="56aad-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="56aad-105">Overview</span></span>
<span data-ttu-id="56aad-106">Se le applicazioni funzionino ma vedrai una latenza prolungata, è possibile alcune modifiche di lieve entità nella topologia di rete che è possibile prendere in considerazione velocità hello tooimprove.</span><span class="sxs-lookup"><span data-stu-id="56aad-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="56aad-107">Per una versione di valutazione di diverse topologie, vedere hello [documento considerazioni sulla rete](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="56aad-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="56aad-108">Se queste considerazioni non sono utili, purtroppo al momento non abbiamo altri consigli per ottimizzare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="56aad-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="56aad-109">Come servizio Proxy applicazione hello espande toomore data Center che possono essere tooyou più vicino, è possibile avviare direttamente latenza toosee migliorata.</span><span class="sxs-lookup"><span data-stu-id="56aad-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="56aad-110">Centra elenco completo di hello toosee dei dati di Azure, è possibile visualizzare hello [pagina di prova di latenza](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="56aad-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="56aad-111">Hello data center con il servizio Proxy di applicazione hello è disponibile con hello [connettore porte Test strumento](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="56aad-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="56aad-112">Commenti sulle posizioni dei data center del proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="56aad-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="56aad-113">È possibile data center di Azure che non include ancora Proxy dell'applicazione ma potrebbe causare miglioramento latenza grande tooa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="56aad-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="56aad-114">posizione in Hello del data center < aadapfeedback@microsoft.com > per poterlo utilizzare tooplan i commenti e suggerimenti quando si espande.</span><span class="sxs-lookup"><span data-stu-id="56aad-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="56aad-115">Si stanno lavorando alcune funzionalità aggiuntive che consentono di migliorare latenza hello per i tenant che attualmente vedere latenze lungo e che documentazione tooshare una volta disponibile.</span><span class="sxs-lookup"><span data-stu-id="56aad-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56aad-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56aad-116">Next steps</span></span>
[<span data-ttu-id="56aad-117">Usare server proxy locali esistenti</span><span class="sxs-lookup"><span data-stu-id="56aad-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
