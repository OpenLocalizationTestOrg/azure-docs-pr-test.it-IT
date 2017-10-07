---
title: Documentazione di Operations Management Suite (OMS) - esercitazioni aaaAzure | Documenti Microsoft
description: "Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. In questo articolo identifica diversi servizi hello inclusi in OMS e vengono forniti i collegamenti tootheir dettagliate contenuto."
services: operations-management-suite
author: carolz
manager: carolz
layout: LandingPage
ms.assetid: 
ms.service: operations-management-suite
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.date: 01/23/2017
ms.author: carolz
ms.openlocfilehash: 11a8f5ecb3d84aed90554510fc1bb43320fdebb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Informazioni su Operations Management Suite (OMS)
Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.  Poiché OMS viene implementato come servizio basato sul cloud, è possibile renderlo operativo rapidamente con un investimento minimo nei servizi di infrastruttura.  Le nuove funzionalità vengono rese disponibili automaticamente, evitando così i costi di manutenzione e di aggiornamento.

Inoltre tooproviding importanti servizi in modo autonomo, OMS possono integrare con componenti di System Center come System Center Operations Manager tooextend gli investimenti esistenti di gestione in cloud hello.  System Center e OMS possono essere usati insieme tooprovide esperienza di una gestione ibrida completa.

Hello le sezioni seguenti fornita una descrizione di alto livello di hello varie aree di valore dei servizi OMS e hello che le implementano.  È possibile fare riferimento tooOMS architettura per una panoramica dei diversi componenti di OMS hello prima revisione hello documentazione per ogni dettagliata.

## <a name="insight-and-analyticsmediaoperations-management-suite-overviewicon-insight-analyticspng-insight-and-analytics"></a>![Insight & Analytics](media/operations-management-suite-overview/icon-insight-analytics.png) Insight & Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) consente di raccogliere, correlare e cercare i dati di prestazioni e log generati da sistemi operativi e applicazioni e di agire su tali dati. Fornisce informazioni operative in tempo reale tramite la ricerca integrata e dashboard personalizzati tooreadily analizzare milioni di record in tutti i carichi di lavoro e i server indipendentemente dalla loro posizione fisica.

È possibile aggiungere facilmente soluzioni tooLog Analitica che definiscono toobe dati raccolti e hello logica per la relativa analisi.  Le soluzioni possono includere funzionalità aggiuntive che vengono rese automaticamente disponibili tooagents con una quantità minima o alcuna configurazione.  Inoltre toousing gli strumenti di analisi forniti dalle singole soluzioni, è possibile eseguire ricerche personalizzate nell'intero set di dati hello nei dati toocorrelate ordine tra i sistemi e applicazioni.  

## <a name="automation--controlmediaoperations-management-suite-overviewicon-automation-controlpng-automation--control"></a>![Automation & Control](media/operations-management-suite-overview/icon-automation-control.png) Automation & Control
Automazione di Azure automatizza i processi amministrativi con [runbook](../automation/automation-runbook-types.md) che sono basati su PowerShell ed eseguiti nel cloud di Azure hello.  I runbook possono accedere a qualsiasi prodotto o servizio che può essere gestito con PowerShell, incluse risorse in altri cloud come Amazon Web Services (AWS).  I runbook possono inoltre essere eseguiti in un server delle risorse locali di center toomanage dati locali.

Automazione di Azure consente la gestione della configurazione con [PowerShell DSC](../automation/automation-dsc-overview.md).  È possibile creare e gestire risorse DSC ospitate in Azure e applicarle toodefine sistemi locali e toocloud e applicare automaticamente la loro configurazione.

## <a name="protection-and-recoverymediaoperations-management-suite-overviewicon-protection-recoverypng-protection-and-disaster-recovery"></a>![Protezione e ripristino](media/operations-management-suite-overview/icon-protection-recovery.png) Protezione e ripristino di emergenza
[Backup di Azure](http://azure.microsoft.com/documentation/services/backup) protegge i dati delle applicazioni e li conserva per anni, senza investimenti di capitali e con costi operativi minimi.  Può eseguire il backup dei dati dal server Windows fisici e virtuali nei carichi di lavoro tooapplication aggiunta, ad esempio SQL Server e SharePoint.  Può essere utilizzato anche da tooAzure dati tooreplicate protetto di System Center Data Protection Manager (DPM) per la ridondanza e archiviazione a lungo termine.

[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) contribuisce tooyour continuità aziendale e una strategia di ripristino di emergenza gestendo la replica, failover e ripristino di macchine virtuali di Hyper-V locali, macchine virtuali VMware e fisici Windows / Server Linux. È possibile replicare macchine tooa data center secondario o estendere il data center replicandole tooAzure. Site Recovery fornisce inoltre funzionalità per semplificare il failover e il ripristino dei carichi di lavoro. Si integra con i meccanismi di ripristino di emergenza come SQL Server AlwaysOn e prevede piani di ripristino per il failover semplificato dei carichi di lavoro organizzati su più livelli in diversi computer.

## <a name="oms-security-and-compliancemediaoperations-management-suite-overviewicon-security-compliancepng-security-and-compliance"></a>![Sicurezza e conformità di OMS](media/operations-management-suite-overview/icon-security-compliance.png) Sicurezza e conformità
Sicurezza e conformità consente di identificare, valutare e ridurre i rischi di sicurezza tooyour infrastruttura.  Queste funzionalità di OMS vengono implementate tramite diverse soluzioni in Analitica di Log che consentono di analizzare i dati di log e la configurazione da agente sistemi tooassist è di garantire hello sicurezza continuativa dell'ambiente.

* Hello [soluzione Security and Audit](oms-security-getting-started.md) raccoglie e analizza gli eventi di sicurezza in un'attività sospetta tooidentify sistemi gestiti.
* Hello [soluzione Antimalware](../log-analytics/log-analytics-malware.md) segnala stato hello della protezione antimalware nei sistemi gestiti.  
* Hello soluzione System Updates esegue un'analisi degli aggiornamenti della sicurezza hello e altri aggiornamenti nei sistemi gestiti in modo da identificare facilmente i sistemi che richiedono l'applicazione di patch.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)
* Informazioni su [Automazione di Azure](../automation/automation-intro.md)
* Informazioni su [Backup di Azure](http://azure.microsoft.com/documentation/services/backup)
* Informazioni su [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)

