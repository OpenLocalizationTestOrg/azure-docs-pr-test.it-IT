---
title: Accessi da dispositivi potenzialmente infetti
description: Un report che include i tentativi di accesso che sono stati effettuati da dispositivi in cui potrebbe essere in esecuzione un software dannoso (malware).
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="80474-103">Accessi da dispositivi potenzialmente infetti</span><span class="sxs-lookup"><span data-stu-id="80474-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="80474-104">Questo report tenta di identificare i dispositivi degli utenti che sono stati infettati e fanno ora parte di una botnet.</span><span class="sxs-lookup"><span data-stu-id="80474-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="80474-105">Gli indirizzi IP di accesso degli utenti vengono messi in correlazione con gli indirizzi IP in contatto con i server della botnet.</span><span class="sxs-lookup"><span data-stu-id="80474-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="80474-106">Raccomandazione: questo report contrassegna gli indirizzi IP, non i dispositivi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="80474-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="80474-107">Per verificarlo, si consiglia di contattare l'utente e di eseguire la scansione di tutti i dispositivi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="80474-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="80474-108">È inoltre possibile che un dispositivo personale dell'utente sia stato infettato o che un altro utente, che stava usando lo stesso indirizzo IP, abbia un dispositivo infetto.</span><span class="sxs-lookup"><span data-stu-id="80474-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="80474-109">Per altre informazioni su come risolvere problemi correlati alle infezioni malware, vedere [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span><span class="sxs-lookup"><span data-stu-id="80474-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![Accessi da dispositivi potenzialmente infetti](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

