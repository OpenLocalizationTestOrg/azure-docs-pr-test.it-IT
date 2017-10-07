---
title: aaaPrerequisites per l'adozione di Azure ExpressRoute | Documenti Microsoft
description: Questa pagina fornisce un elenco di requisiti toobe soddisfatti prima di ordinare un circuito ExpressRoute di Azure.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Prerequisiti di ExpressRoute ed elenco di controllo
tooconnect tooMicrosoft cloud services tramite ExpressRoute, occorre tooverify tale hello seguendo i requisiti elencati in hello le sezioni seguenti sono stati soddisfatti.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Account Azure
* Un account Microsoft Azure valido e attivo. Questo account è obbligatorio tooset backup hello circuito ExpressRoute. I circuiti ExpressRoute sono risorse all'interno di sottoscrizioni di Azure. Una sottoscrizione di Azure è un requisito, anche se la connettività è limitato toonon-Microsoft servizi cloud di Azure, ad esempio servizi di Office 365 e Dynamics 365.
* Una sottoscrizione di Office 365 attiva (se si usano servizi di Office 365). Per ulteriori informazioni, vedere hello [requisiti specifici di Office 365](#office-365-specific-requirements) sezione di questo articolo.

## <a name="connectivity-provider"></a>Provider di connettività

* È possibile utilizzare un [partner connettività ExpressRoute](expressroute-locations.md#partners) tooconnect toohello cloud Microsoft. È possibile configurare una connessione tra la rete locale e Microsoft in [tre modi](expressroute-introduction.md)diversi.
* Se il provider non è un partner di connettività di ExpressRoute, è comunque possibile connettersi toohello Microsoft cloud tramite un [provider di cloud exchange](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Requisiti di rete
* **Connettività ridondante**: non è stato definito alcun requisito di ridondanza per la connettività fisica con il provider. Microsoft richiede ridondanza toobe di sessioni BGP impostare tra i router e i router peer hello, Microsoft, anche se sono presenti solo [una connessione fisica tooa cloud exchange](expressroute-faqs.md#onep2plink).
* **Routing**: a seconda della modalità di connessione toohello Cloud Microsoft, si o del provider necessario tooset backup e gestire le sessioni BGP hello per [domini di routing](expressroute-circuit-peerings.md). Alcuni provider di connettività Ethernet o provider Cloud Exchange possono offrire la gestione BGP come servizio a valore aggiunto.
* **NAT**: Microsoft accetta solo indirizzi IP pubblici tramite peer Microsoft. Se si utilizza indirizzi IP nella rete locale, si o del provider necessario tootranslate hello privata degli indirizzi IP gli indirizzi IP pubblici toohello [utilizzando hello NAT](expressroute-nat.md).
* **QoS**: Skype for Business include diversi servizi, ad esempio voce, video o testo, che richiedono una gestione QoS differenziata. Sia il provider deve seguire hello [requisiti QoS](expressroute-qos.md).
* **Sicurezza di rete**: considerare [sicurezza di rete](../best-practices-network-security.md) quando ci si connette toohello Microsoft Cloud tramite ExpressRoute.

## <a name="office-365"></a>Office 365
Se si prevede di ExpressRoute tooenable Office 365, esaminare hello seguenti documenti per ulteriori informazioni sui requisiti di Office 365.

* [Panoramica di ExpressRoute per Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Routing con ExpressRoute per Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [URL e intervalli di indirizzi IP per Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Pianificazione della rete e ottimizzazione delle prestazioni per Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Calcolatori e strumenti per la larghezza di banda di rete](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Integrazione di Office 365 con ambienti locali](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Video di training avanzato su ExpressRoute in Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Se si intende tooenable Dynamics 365 ExpressRoute, esaminare i seguenti documenti per ulteriori informazioni su Dynamics 365 hello

* [White paper su Dynamics 365 ed ExpressRoute](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [URL](https://support.microsoft.com/kb/2655102) e [intervalli di indirizzi IP per Dynamics 365](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
* Individuare un partner per la connettività ad ExpressRoute. Vedere [Partner e località di peering per Azure ExpressRoute](expressroute-locations.md).
* Fare riferimento toorequirements per [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurare la connessione ExpressRoute.
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurare il routing](expressroute-howto-routing-classic.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md)
