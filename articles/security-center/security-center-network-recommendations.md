---
title: aaaProtecting la rete in Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento illustra le raccomandazioni presenti nel Centro sicurezza di Azure che facilitano la protezione della rete di Azure e garantiscano la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Protezione della rete nel Centro sicurezza di Azure
Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato indicazioni che consentono di eseguire il processo di hello di configurazione dei controlli di hello necessita.  Consigli si applicano a tipi di risorse tooAzure: macchine virtuali (VM), rete, SQL e le applicazioni.

Questo articolo illustra indicazioni applicabili tooyour rete.  Le raccomandazioni per le risorse di rete sono incentrate sui firewall di nuova generazione, sui gruppi di sicurezza di rete, sulla configurazione delle regole di traffico in ingresso e altro ancora.  Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere indicazioni di rete disponibile hello e ciascuna di esse cosa se lo si applica.

## <a name="available-network-recommendations"></a>Indicazioni disponibili per la rete
| Raccomandazione | Descrizione |
| --- | --- |
| [Aggiungi un firewall di nuova generazione](security-center-add-next-generation-firewall.md) |Consiglia di aggiungere un Firewall di generazione successiva (NGFW) da un tooincrease partner Microsoft i meccanismi di protezione. |
| [Indirizza il traffico solo tramite il firewall di nuova generazione](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Consiglia di configurare regole di gruppo () sicurezza di rete che impongono il traffico in entrata tooyour VM tramite il NGFW. |
| [Abilita i gruppi di sicurezza di rete sulle subnet o sulle macchine virtuali](security-center-enable-network-security-groups.md) |Consiglia di attivare i gruppo di sicurezza di rete sulle subnet o sulle macchine virtuali. |
| [Limita l'accesso tramite un endpoint con connessione Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Consiglia di configurare le regole del traffico in ingresso per i gruppi di sicurezza di rete. |

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni sui suggerimenti che si applicano tooother tipi di risorse di Azure, vedere l'esempio hello:

* [Protezione delle macchine virtuali nel Centro sicurezza di Azure](security-center-virtual-machine-recommendations.md)
* [Protecting your applications in Azure Security Center](security-center-application-recommendations.md)
* [Protezione del servizio SQL di Azure nel Centro sicurezza di Azure](security-center-sql-service-recommendations.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
