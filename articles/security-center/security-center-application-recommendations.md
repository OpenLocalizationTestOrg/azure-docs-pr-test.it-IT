---
title: aaaProtecting le applicazioni nel Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento illustra le raccomandazioni presenti nel Centro sicurezza di Azure che facilitano la protezione delle applicazioni Azure e garantiscono la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Protezione delle applicazioni nel Centro sicurezza di Azure
Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato indicazioni che consentono di eseguire il processo di hello di configurazione dei controlli di hello necessita.  Consigli si applicano a tipi di risorse tooAzure: macchine virtuali (VM), rete, SQL e le applicazioni.

Questo articolo illustra indicazioni applicabili tooapplications.  Le raccomandazioni relative alle applicazioni sono incentrate sulla distribuzione di un web application firewall.  Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere indicazioni disponibili applicazione hello e la funzione ognuno se lo si applica.

## <a name="available-application-recommendations"></a>Raccomandazioni disponibili sulle applicazioni
| Raccomandazione | Descrizione |
| --- | --- |
| [Aggiungere un Web Application Firewall](security-center-add-web-application-firewall.md) |Suggerisce di distribuire un Web application firewall (WAF) per gli endpoint Web. Viene visualizzata una raccomandazione WAF per qualsiasi IP pubblico (IP a livello di istanza o IP con carico bilanciato) cui è associato un gruppo di sicurezza di rete con porte Web in ingresso aperte (80, 443).</br></br>Centro sicurezza PC consiglia che si provisioning un toohelp WAF difendersi da attacchi di applicazioni web nelle macchine virtuali e sull'ambiente di servizio App di destinazione. Un Ambiente del servizio app è un'opzione del piano di servizio [Premium](https://azure.microsoft.com/pricing/details/app-service/) del Servizio app di Azure che offre un ambiente completamente isolato e dedicato per eseguire in modo sicuro tutte le app del servizio. toolearn ulteriori informazioni su ASE, vedere hello [documentazione dell'ambiente del servizio App](../app-service/app-service-app-service-environments-readme.md).</br></br>È possibile proteggere nel Centro protezione di più applicazioni web tramite l'aggiunta di queste applicazioni tooyour WAF le distribuzioni esistenti. |
| [Finalizza la protezione dell'applicazione](security-center-add-web-application-firewall.md#finalize-application-protection) |configurazione di hello toocomplete di un WAF, il traffico deve essere reindirizzato toohello WAF accessorio. Seguendo queste indicazioni completa delle modifiche di installazione necessari hello. |

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni sui suggerimenti che si applicano tooother tipi di risorse di Azure, vedere l'esempio hello:

* [Protezione delle macchine virtuali nel Centro sicurezza di Azure](security-center-virtual-machine-recommendations.md)
* [Protezione della rete nel Centro sicurezza di Azure](security-center-network-recommendations.md)
* [Protezione del servizio SQL di Azure nel Centro sicurezza di Azure](security-center-sql-service-recommendations.md)

toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.
