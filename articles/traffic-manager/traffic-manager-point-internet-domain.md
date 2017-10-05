---
title: Impostare un dominio Internet aziendale in modo che punti a un nome di dominio di Gestione traffico | Documentazione Microsoft
description: In questo articolo vengono fornite istruzioni per scegliere il nome di dominio aziendale per un nome di dominio di Gestione traffico.
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
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a><span data-ttu-id="b8d76-103">Impostare un dominio Internet aziendale in modo che punti a un dominio di Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="b8d76-103">Point a company Internet domain to an Azure Traffic Manager domain</span></span>

<span data-ttu-id="b8d76-104">Quando si crea un profilo di Gestione traffico, Azure assegna automaticamente un nome DNS per tale profilo.</span><span class="sxs-lookup"><span data-stu-id="b8d76-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="b8d76-105">Per usare un nome dalla zona DNS, creare un record DNS CNAME che esegua il mapping al nome di dominio del profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="b8d76-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="b8d76-106">È possibile visualizzare il nome di dominio di Gestione traffico nella sezione **Generale** nella pagina di configurazione del profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="b8d76-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span></span>

<span data-ttu-id="b8d76-107">Ad esempio, per scegliere il nome www.contoso.com per il nome DNS di Gestione traffico contoso.trafficmanager.net, è possibile creare il record di risorse DNS seguente:</span><span class="sxs-lookup"><span data-stu-id="b8d76-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="b8d76-108">Tutto il traffico indirizzato a *www.contoso.com* viene reindirizzato a *contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="b8d76-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8d76-109">Non è possibile scegliere un dominio di secondo livello, come *contoso.com*, per il dominio di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="b8d76-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span></span> <span data-ttu-id="b8d76-110">Gli standard di protocollo DNS non consentono record CNAME per i nomi di dominio di secondo livello.</span><span class="sxs-lookup"><span data-stu-id="b8d76-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8d76-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8d76-111">Next steps</span></span>

* [<span data-ttu-id="b8d76-112">Metodi di routing di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="b8d76-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="b8d76-113">Gestione traffico: disabilitare, abilitare o eliminare un profilo</span><span class="sxs-lookup"><span data-stu-id="b8d76-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="b8d76-114">Gestione traffico: disabilitare o abilitare un endpoint</span><span class="sxs-lookup"><span data-stu-id="b8d76-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
