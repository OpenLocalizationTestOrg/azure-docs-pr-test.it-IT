---
title: un nome di dominio aziendale Internet dominio tooa Traffic Manager aaaPoint | Documenti Microsoft
description: "In questo articolo consentirà di scegliere il nome di dominio della società dominio nome tooa Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="a8aa6-103">Scegliere un dominio Internet della società dominio tooan Traffic Manager di Azure</span><span class="sxs-lookup"><span data-stu-id="a8aa6-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="a8aa6-104">Quando si crea un profilo di Gestione traffico, Azure assegna automaticamente un nome DNS per tale profilo.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="a8aa6-105">toouse un nome dalla zona DNS, creare un record DNS CNAME che associa il nome di dominio toohello del profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="a8aa6-106">È possibile trovare un nome di dominio di Traffic Manager hello in hello **generale** sezione nella pagina di configurazione hello di hello profilo di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="a8aa6-107">Ad esempio www.contoso.com nome toopoint toohello contoso.trafficmanager.net nome DNS di Traffic Manager, si creerà hello seguenti record di risorse DNS:</span><span class="sxs-lookup"><span data-stu-id="a8aa6-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="a8aa6-108">Tutto il traffico richiede troppo*www.contoso.com* vengono indirizzati troppo*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8aa6-109">Non è possibile puntare un dominio di secondo livello, ad esempio *contoso.com*, toohello dominio di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="a8aa6-110">Gli standard di protocollo DNS non consentono record CNAME per i nomi di dominio di secondo livello.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8aa6-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8aa6-111">Next steps</span></span>

* [<span data-ttu-id="a8aa6-112">Metodi di routing di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="a8aa6-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="a8aa6-113">Gestione traffico: disabilitare, abilitare o eliminare un profilo</span><span class="sxs-lookup"><span data-stu-id="a8aa6-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="a8aa6-114">Gestione traffico: disabilitare o abilitare un endpoint</span><span class="sxs-lookup"><span data-stu-id="a8aa6-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
