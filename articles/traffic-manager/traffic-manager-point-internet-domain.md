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
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Scegliere un dominio Internet della società dominio tooan Traffic Manager di Azure

Quando si crea un profilo di Gestione traffico, Azure assegna automaticamente un nome DNS per tale profilo. toouse un nome dalla zona DNS, creare un record DNS CNAME che associa il nome di dominio toohello del profilo di Traffic Manager. È possibile trovare un nome di dominio di Traffic Manager hello in hello **generale** sezione nella pagina di configurazione hello di hello profilo di gestione traffico.

Ad esempio www.contoso.com nome toopoint toohello contoso.trafficmanager.net nome DNS di Traffic Manager, si creerà hello seguenti record di risorse DNS:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Tutto il traffico richiede troppo*www.contoso.com* vengono indirizzati troppo*contoso.trafficmanager.net*.

> [!IMPORTANT]
> Non è possibile puntare un dominio di secondo livello, ad esempio *contoso.com*, toohello dominio di Traffic Manager. Gli standard di protocollo DNS non consentono record CNAME per i nomi di dominio di secondo livello.

## <a name="next-steps"></a>Passaggi successivi

* [Metodi di routing di Gestione traffico](traffic-manager-routing-methods.md)
* [Gestione traffico: disabilitare, abilitare o eliminare un profilo](disable-enable-or-delete-a-profile.md)
* [Gestione traffico: disabilitare o abilitare un endpoint](disable-or-enable-an-endpoint.md)
