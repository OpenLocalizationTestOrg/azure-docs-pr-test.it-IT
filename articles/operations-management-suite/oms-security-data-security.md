---
title: aaaOperations gestione gruppo di sicurezza e protezione dei dati di controllo soluzione | Documenti Microsoft
description: Questo documento illustra il modo in cui i dati vengono gestiti e protetti nella soluzione Sicurezza e controllo di Operations Management Suite.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Sicurezza dei dati della soluzione Sicurezza e controllo di Operations Management Suite
i clienti toohelp impedire, rilevare e rispondere toothreats, [soluzione di controllo e protezione di Operations Management Suite (OMS)](operations-management-suite-overview.md) raccoglie ed elabora i dati sulle risorse, che includono:

* Registri eventi sicurezza
* Tracciamento degli eventi di Windows (ETW)
* Eventi di controllo AppLocker
* Log di Windows Firewall
* Eventi di Advanced Threat Analytics
* Risultati della valutazione baseline
* Risultati di Antimalware Assessment
* Risultati della valutazione di aggiornamenti/patch
* Flussi i registri di sistema che sono abilitati in modo esplicito sull'agente hello

Rendiamo impegni sicuro tooprotect hello privacy e protezione dei dati. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio.
Questo articolo illustra il modo in cui i dati vengono gestiti e protetti nella soluzione Sicurezza e controllo di OMS.

## <a name="data-sources"></a>Origini dati
Soluzione di controllo e sicurezza OMS analizzare i dati dalle macchine virtuali e i computer fisici in cui è installato l'agente OMS hello. La soluzione Sicurezza e controllo di OMS può raccogliere informazioni di configurazione sugli eventi di sicurezza, ad esempio gli eventi Windows, i log di controllo, i log di IIS e i messaggi syslog. Esempi di tali dati sono: tipo e versione del sistema operativo, processi in esecuzione, nome computer, indirizzi IP, utente connesso e ID tenant.  

## <a name="data-protection"></a>Protezione dati
**La separazione dei dati**: dati vengono mantenuti separati logicamente in ogni componente servizio hello. Tutti i dati vengono contrassegnati in base all'organizzazione. Tale contrassegno persiste per tutto hello del ciclo di vita dei dati e viene applicato a ogni livello del servizio hello. 

**Accesso ai dati**: tooprovide consigli relativi alla sicurezza e provare a potenziali minacce alla sicurezza, personale Microsoft potrebbero accedere a informazioni raccolte o analizzati dai servizi. È conforme toohello [condizioni per i servizi Online Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [informativa sulla Privacy](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), quale stato che Microsoft non utilizza i dati dei clienti o derivare da esso per annunci o simili a scopo commerciale. consigli sulla sicurezza tooprovide e analizzare potenziali minacce alla sicurezza, il personale di Microsoft possono accedere a informazioni raccolte o analizzati dai servizi. Utilizziamo solo i dati dei clienti come tooprovide necessari con Azure servizi, inclusi motivi compatibile con tali servizi. Mantenere tutti i dati personalizzati tooyour diritti.

**Utilizzo di dati**: Microsoft utilizza i modelli e sulle minacce visualizzata in più tenant tooenhance la funzionalità di rilevamento e prevenzione; avviene in conformità con impegni di privacy hello descritto in questo [sulla Privacy Istruzione](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Percorso dei dati è configurata a livello di area di lavoro OMS hello, durante la creazione dell'area di lavoro hello, che fa parte del processo configurazione OMS Security and Audit iniziale hello.
> 
> 

## <a name="see-also"></a>Vedere anche
Questo documento illustra in che modo vengono gestiti e protetti i dati in OMS. toolearn ulteriori informazioni su sicurezza OMS e la soluzione di controllo, vedere:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

