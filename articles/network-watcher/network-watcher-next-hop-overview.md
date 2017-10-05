---
title: Introduzione all'hop successivo in Azure Network Watcher | Microsoft Docs
description: "Questa pagina fornisce una panoramica della funzionalità hop successivo di Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="d491a-103">Introduzione all'hop successivo in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d491a-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="d491a-104">Il traffico proveniente da una macchina virtuale viene inviato a una destinazione in base alle route valide associate alla scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="d491a-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="d491a-105">L'hop successivo ottiene il tipo di hop successivo e l'indirizzo IP di un pacchetto da una macchina virtuale e una scheda di interfaccia di rete specifiche.</span><span class="sxs-lookup"><span data-stu-id="d491a-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="d491a-106">Ciò consente di determinare se il pacchetto viene indirizzato a destinazione o se il traffico viene inviato a un black hole.</span><span class="sxs-lookup"><span data-stu-id="d491a-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="d491a-107">Una configurazione errata delle route da parte dell'utente, in cui il traffico viene indirizzato a un percorso locale oppure a un dispositivo virtuale, può causare problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="d491a-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="d491a-108">L'hop successivo restituisce anche la tabella di route associata all'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="d491a-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="d491a-109">Quando si eseguono query su un hop successivo, viene restituita la route, se definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d491a-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="d491a-110">In caso contrario l'hop successivo restituisce la route di sistema.</span><span class="sxs-lookup"><span data-stu-id="d491a-110">Otherwise Next hop returns "System Route".</span></span>

![Panoramica dell'hop successivo][1]

<span data-ttu-id="d491a-112">Di seguito è riportato un elenco dei tipi di hop successivo che possono essere restituiti dalle query sull'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="d491a-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="d491a-113">Internet</span><span class="sxs-lookup"><span data-stu-id="d491a-113">Internet</span></span>
* <span data-ttu-id="d491a-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="d491a-114">VirtualAppliance</span></span>
* <span data-ttu-id="d491a-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="d491a-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="d491a-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="d491a-116">VnetLocal</span></span>
* <span data-ttu-id="d491a-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="d491a-117">HyperNetGateway</span></span>
* <span data-ttu-id="d491a-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="d491a-118">VnetPeering</span></span>
* <span data-ttu-id="d491a-119">None</span><span class="sxs-lookup"><span data-stu-id="d491a-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="d491a-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d491a-120">Next steps</span></span>

<span data-ttu-id="d491a-121">Per informazioni su come usare l'hop successivo per rilevare i problemi di connettività di rete, vedere l'articolo relativo alla [verifica dell'hop successivo in una macchina virtuale](network-watcher-check-next-hop-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d491a-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













