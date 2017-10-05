---
title: 'Larghezza di banda di rete di Azure RemoteApp: linee guida generali | Microsoft Docs'
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="a5827-103">Larghezza di banda di rete di Azure RemoteApp: linee guida generali (se non è possibile verificare direttamente)</span><span class="sxs-lookup"><span data-stu-id="a5827-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5827-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="a5827-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a5827-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="a5827-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a5827-106">Se non si dispone del tempo o non si ha la possibilità di eseguire il [test della larghezza di banda della rete](remoteapp-bandwidthtests.md) per Azure RemoteApp, di seguito sono riportate alcune linee guida piuttosto generiche che consentono di stimare la larghezza di banda di rete per utente.</span><span class="sxs-lookup"><span data-stu-id="a5827-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="a5827-107">Se il proprio scenario è una combinazione di questi, non è consigliabile un valore minore di (o uguale a) 10 MB/s come larghezza di banda MINIMA per le app moderne connesse a Internet in un ambiente remoto.</span><span class="sxs-lookup"><span data-stu-id="a5827-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="a5827-108">Questo però, come si è detto, non garantisce un'esperienza utente superiore alla media.</span><span class="sxs-lookup"><span data-stu-id="a5827-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="a5827-109">Presentazioni complesse, presentazioni semplici</span><span class="sxs-lookup"><span data-stu-id="a5827-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="a5827-110">Azure RemoteApp funziona meglio in una LAN a 100 MB.</span><span class="sxs-lookup"><span data-stu-id="a5827-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="a5827-111">Con un profilo di rete di 10 MB/s, quando l'instabilità oltre 120 ms supera il 5%, l'esperienza utente è di qualità media.</span><span class="sxs-lookup"><span data-stu-id="a5827-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="a5827-112">Con 1 MB/s la differenza è evidente. Ad esempio, in una presentazione, l'utente potrebbe non vedere affatto le transizioni animate perché vengono ignorati numerosi fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="a5827-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="a5827-113">Internet Explorer, PDF misto, PDF, testo</span><span class="sxs-lookup"><span data-stu-id="a5827-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="a5827-114">Un profilo di rete di 10 MB/s è simile a una LAN in molti aspetti.</span><span class="sxs-lookup"><span data-stu-id="a5827-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="a5827-115">1 MB/s offre un'esperienza accettabile, anche se potrebbe verificarsi una certa instabilità quando un utente scorre un documento mentre sono visualizzate immagini sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="a5827-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="a5827-116">Video Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="a5827-116">Flash video (YouTube)</span></span>
<span data-ttu-id="a5827-117">Una LAN da 100 MB/s garantisce un'esperienza ottimale, mentre una larghezza di banda di 10 MB/s è accettabile, nel senso che riesce a stare al passo con la frequenza dei fotogrammi ma l'instabilità aumenta.</span><span class="sxs-lookup"><span data-stu-id="a5827-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="a5827-118">Con 1 MB/s l'instabilità è molto elevata ed evidente.</span><span class="sxs-lookup"><span data-stu-id="a5827-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="a5827-119">Digitazione in Word (input remoto in Word)</span><span class="sxs-lookup"><span data-stu-id="a5827-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="a5827-120">Si tratta di uno scenario con un utilizzo ridotto della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="a5827-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="a5827-121">Con 256 KB/s l'esperienza ha la stessa qualità di quella offerta da una LAN.</span><span class="sxs-lookup"><span data-stu-id="a5827-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a5827-122">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="a5827-122">Learn more</span></span>
* [<span data-ttu-id="a5827-123">Uso previsto della larghezza di banda di rete di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a5827-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="a5827-124">Azure RemoteApp - In che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?</span><span class="sxs-lookup"><span data-stu-id="a5827-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="a5827-125">Azure RemoteApp: scenari comuni di test relativi all'utilizzo della larghezza di banda di rete</span><span class="sxs-lookup"><span data-stu-id="a5827-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

