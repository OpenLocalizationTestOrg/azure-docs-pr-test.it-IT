---
title: larghezza di banda RemoteApp aaaAzure - linee guida generali | Documenti Microsoft
description: Linee guida di base sulla larghezza di banda di rete per le raccolte e le app Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="7d86b-103">Larghezza di banda di rete di Azure RemoteApp: linee guida generali (se non è possibile verificare direttamente)</span><span class="sxs-lookup"><span data-stu-id="7d86b-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d86b-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="7d86b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7d86b-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="7d86b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7d86b-106">Se non si dispone hello toorun ora o la funzionalità di hello [test della larghezza di banda di rete](remoteapp-bandwidthtests.md) per Azure RemoteApp, di seguito sono riportate alcune linee guida piuttosto generica che consentono di stimare la larghezza di banda di rete per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="7d86b-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="7d86b-107">Se si dispone di una combinazione di questi scenari, non è consigliabile un valore minore di (o uguale a) 10 MB/s come hello larghezza di banda minima per le app moderne in un ambiente remoto connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="7d86b-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="7d86b-108">Questo però, come si è detto, non garantisce un'esperienza utente superiore alla media.</span><span class="sxs-lookup"><span data-stu-id="7d86b-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="7d86b-109">Presentazioni complesse, presentazioni semplici</span><span class="sxs-lookup"><span data-stu-id="7d86b-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="7d86b-110">Azure RemoteApp funziona meglio in una LAN a 100 MB.</span><span class="sxs-lookup"><span data-stu-id="7d86b-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="7d86b-111">In hello 10 MB/s rete profilo quando più del 5%, utente hello instabilità sopra ms 120 visualizzeranno un'esperienza di Media.</span><span class="sxs-lookup"><span data-stu-id="7d86b-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="7d86b-112">A hello di 1 MB/s diverso è ritornare - ad esempio, in una presentazione, utente hello potrebbe non essere visibili transizioni animate affatto perché i frame vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="7d86b-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="7d86b-113">Internet Explorer, PDF misto, PDF, testo</span><span class="sxs-lookup"><span data-stu-id="7d86b-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="7d86b-114">Profilo di rete 10 MB/s è tooLAN Chiudi nella maggior parte degli aspetti.</span><span class="sxs-lookup"><span data-stu-id="7d86b-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="7d86b-115">1 MB/s fornirà un'esperienza di OK, sebbene vi siano alcune instabilità quando un utente scorre mentre vi sono immagini nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="7d86b-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="7d86b-116">Video Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="7d86b-116">Flash video (YouTube)</span></span>
<span data-ttu-id="7d86b-117">100 MB/s LAN fornisce un'esperienza ottimale hello, mentre i 10 MB/s è accettabile (a indicare che è sincronizzato con frequenza dei fotogrammi hello, ma aumenta di variazione).</span><span class="sxs-lookup"><span data-stu-id="7d86b-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="7d86b-118">Con 1 MB/s l'instabilità è molto elevata ed evidente.</span><span class="sxs-lookup"><span data-stu-id="7d86b-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="7d86b-119">Digitazione in Word (input remoto in Word)</span><span class="sxs-lookup"><span data-stu-id="7d86b-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="7d86b-120">Si tratta di uno scenario con un utilizzo ridotto della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="7d86b-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="7d86b-121">Con 256 KB/s l'esperienza ha la stessa qualità di quella offerta da una LAN.</span><span class="sxs-lookup"><span data-stu-id="7d86b-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7d86b-122">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="7d86b-122">Learn more</span></span>
* [<span data-ttu-id="7d86b-123">Uso previsto della larghezza di banda di rete di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7d86b-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="7d86b-124">Azure RemoteApp - In che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?</span><span class="sxs-lookup"><span data-stu-id="7d86b-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="7d86b-125">Azure RemoteApp: scenari comuni di test relativi all'utilizzo della larghezza di banda di rete</span><span class="sxs-lookup"><span data-stu-id="7d86b-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

