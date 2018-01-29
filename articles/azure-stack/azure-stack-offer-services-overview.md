---
title: Offerta di servizi nello Stack di Azure | Documenti Microsoft
description: "Come operatore di cloud, è possibile offrire servizi agli utenti."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 7a54771d99f2719fcc345496b152a5d3acc02121
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a>Panoramica dell'offerta di servizi di Azure Stack

*Si applica a: Azure Stack integrate di sistemi Azure Stack Development Kit*

[Microsoft Azure Stack](azure-stack-poc.md) è una piattaforma di cloud ibrido che consente di offrire servizi dal Data Center. Come provider di servizi, è possibile offrire servizi ai tenant. All'interno di un'azienda o agenzia governativa, è possibile offrire ai propri dipendenti con i servizi locali. I servizi che è possibile recapitare includono, ma non sono limitati a:

- Piattaforma distribuita come un servizio (PaaS) di servizi come servizi App, App Mobile, App per le API, le funzioni dell'API, SQL, MySQL.

È anche possibile combinare i servizi di integrazione e la compilazione di soluzioni complesse per utenti diversi.

Per distribuire questi servizi agli utenti, è necessario creare [piani, offerte e le quote](azure-stack-plan-offer-quota-overview.md). Gli utenti possono eseguire la sottoscrizione per le offerte di utilizzare i servizi.

## <a name="plan-your-service-offers"></a>Pianificare le offerte di servizio

Quando si pianifica le offerte, tenere i seguenti punti presenti:

**Le offerte di prova**: È possibile utilizzare le offerte di prova per attirare nuovi utenti, che quindi è possono eseguire l'aggiornamento a servizi aggiuntivi. Per creare un'offerta di valutazione, creare un piccolo [piano base](azure-stack-plan-offer-quota-overview.md#base-plan) con un piano del componente aggiuntivo facoltativo più grande.

**Pianificazione della capacità**: È possibile evitare che gli utenti selezionandola grandi quantità di risorse e il sistema per tutti gli utenti è sommersa da. Per migliorare le prestazioni, è possibile [configurare i piani con quote](azure-stack-plan-offer-quota-overview.md#plans) all'utilizzo di criteri.

**Delegato provider**: È possibile concedere ad altri utenti la possibilità di creare offerte nell'ambiente in uso. Ad esempio, se si è un provider di servizi, è possibile [delegato](azure-stack-delegated-provider.md) questa possibilità per i rivenditori. In alternativa, se si ha un'organizzazione, è possibile delegare a altre divisioni/controllate.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni sulle offerte, dei piani, le quote e le sottoscrizioni](azure-stack-plan-offer-quota-overview.md)

