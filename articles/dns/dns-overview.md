---
title: aaaOverview di DNS di Azure | Documenti Microsoft
description: Panoramica del servizio di hosting DNS in Microsoft Azure. Ospitare il dominio in Microsoft Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Panoramica di DNS di Azure

Hello Domain Name System o DNS, è responsabile della conversione (o nel risolvere) un sito Web o servizio name tooits indirizzo IP. DNS di Azure è un servizio di hosting per i domini DNS, che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure. Ospitando i domini in Azure, è possibile gestire il servizio DNS i record mediante hello credenziali, API, strumenti e fatturazione come altri servizi di Azure.

![Panoramica del servizio DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Funzionalità

* **Affidabilità e prestazioni**: i domini DNS nel servizio DNS di Azure sono ospitati nella rete globale di Azure dei server dei nomi DNS. Utilizziamo Anycast di rete in modo che ogni query DNS è stata risposta dal server DNS disponibile più vicino di hello. Ciò consente di accelerare le prestazioni e ottenere la disponibilità elevata per il dominio.

* **Perfetta integrazione** -servizio DNS di Azure hello può essere utilizzato toomanage i record DNS per i servizi di Azure e può essere utilizzato tooprovide DNS per le risorse esterne, nonché. DNS di Azure è integrato nel portale di Azure hello e utilizza hello stesse credenziali, fatturazione e il contratto di assistenza come altri servizi di Azure.

* **Sicurezza** -hello servizio DNS di Azure si basa su Gestione risorse di Azure. Usufruisce quindi delle funzionalità di Resource Manager, come il controllo degli accessi in base al ruolo, i log di controllo e il blocco delle risorse. I domini e i record possono essere gestiti tramite hello portale di Azure, i cmdlet di Azure PowerShell e hello multipiattaforma CLI di Azure. Le applicazioni che richiedono la gestione automatica di DNS è possono integrare con il servizio di hello tramite hello SDK e API REST.

DNS di Azure attualmente non supporta l'acquisto dei nomi di dominio. Se si desidera toopurchase domini, è necessario toouse un registrar di nomi di dominio di terze parti. registrar Hello in genere una tariffa small annuale. domini Hello possono quindi essere ospitati in DNS di Azure per la gestione dei record DNS. Vedere [tooAzure un dominio DNS delegato](dns-domain-delegation.md) per informazioni dettagliate.

## <a name="pricing"></a>Prezzi

DNS fatturazione si basa sul numero di hello di zone DNS ospitate in Azure e dal numero di hello di query DNS. ulteriori informazioni sui prezzi visitare toolearn [dei prezzi di Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>domande frequenti

Per domande frequenti su DNS di Azure, vedere hello [domande frequenti su DNS di Azure](dns-faq.md).

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sui record e le zone DNS visitare la pagina [Panoramica delle zone e dei record DNS](dns-zones-records.md).

Informazioni su come troppo[creare una zona DNS](./dns-getstarted-create-dnszone-portal.md) nel sistema DNS di Azure.

Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.

