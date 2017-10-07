---
title: i log aaaIntegrate dalle risorse di Azure in sistemi SIEM | Documenti Microsoft
description: "Informazioni sull'integrazione dei log di Azure, le funzionalità principali e il funzionamento."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Introduzione tooMicrosoft integrazione di log di Azure
Informazioni sull'integrazione dei log di Azure, le funzionalità principali e il funzionamento.

## <a name="overview"></a>Panoramica

Integrazione di log di Azure è una soluzione gratuita che consente di toointegrate registri raw dalle risorse di Azure nei sistemi di informazioni di sicurezza e gestione di eventi (SIEM) locale tooyour.

L'integrazione dei log di Azure raccoglie gli eventi di Windows da log del Visualizzatore eventi di Windows, [log attività di Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [avvisi del Centro sicurezza di Azure](../security-center/security-center-intro.md) e [log di Diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) dalle risorse di Azure. Questa integrazione consente la soluzione SIEM di fornire un dashboard unificato di tutte le risorse, locale o nel cloud hello, in modo che è possibile aggregare, correlare, analizzare e avviso per gli eventi di sicurezza.

>[!NOTE]
In questo momento, ci sono cloud hello è supportato solo commerciale di Azure e Azure per enti pubblici. Gli altri cloud non sono supportati.

![Integrazione dei log di Azure][1]

## <a name="what-logs-can-i-integrate"></a>Quali log è possibile integrare?
Azure produce registrazioni complete per ogni servizio di Azure. Questi log rappresentano tre tipi di log:

* **I registri di controllo/gestione** fornire visibilità hello [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) operazioni CREATE, UPDATE e DELETE. I log attività di Azure sono un esempio di questo tipo di log.
* **Dati piano registri** conferire visibilità ai dati degli eventi di hello generato nell'ambito di utilizzo di hello di una risorsa di Azure. Un esempio di questo tipo di log è hello Visualizzatore eventi di Windows **sistema**, **sicurezza**, e **applicazione** canali in una macchina virtuale di Windows. Un altro esempio è la registrazione di diagnostica configurata tramite Monitor di Azure
* Gli **eventi elaborati** forniscono eventi analizzati e informazioni sugli avvisi elaborate per conto del cliente. Un esempio di questo tipo di evento è Azure Center avvisi di sicurezza, in cui Centro sicurezza di Azure avrà elaborato e analizzati sottoscrizione tooprovide avvisi tooyour rilevanti corrente comportamento di sicurezza.

L'integrazione dei log di Azure supporta ArcSight, QRadar e Splunk. In tutte le circostanze, contattare il tooassess fornitore SIEM se dispongono di un connettore nativo. In alcuni casi, non occorre toouse integrazione di Log di Azure quando connettori nativi sono disponibili. Per ulteriori informazioni sui log supportati tipi, visitare hello domande frequenti.

>[!NOTE]
Durante l'integrazione di Log di Azure è una soluzione disponibile, vi sono costi di archiviazione di Azure risultante dall'archivio informazioni di hello log file.

Assistenza della community è disponibile tramite hello [Forum MSDN di Azure Log integrazione](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). forum di Hello fornisce hello AzLog community hello possibilità toosupport loro domande, le risposte, suggerimenti e consigli su come tooget hello più dal Log di Azure di integrazione. Inoltre, il team di integrazione di Azure Log hello questo forum consente di monitorare e aiutano ogni volta che è possibile.

Si può anche aprire un [richiesta di supporto](../azure-supportability/how-to-create-azure-support-request.md). toodo, selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.

## <a name="next-steps"></a>Passaggi successivi
In questo documento, sono state introdotte tooAzure log integrazione. toolearn informazioni su Azure log integration e tipi di hello di log supportati, vedere hello informazioni seguenti:

* [Integrazione log di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=53324)- Area download per informazioni dettagliate, requisiti di sistema e istruzioni di installazione per l'integrazione dei log di Azure.
* [Introduzione all'integrazione dei log di Azure](security-azure-log-integration-get-started.md) - Questa esercitazione illustra come installare l'integrazione dei log di Azure e integrare i log dall'archiviazione di Azure WAD, i log attività di Azure, gli avvisi del Centro sicurezza di Azure e i log di controllo di Azure Active Directory.
* [Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – questo post di blog viene illustrato come tooconfigure Azure log toowork integrazione con soluzioni di partner Splunk e ArcSight HP, IBM QRadar. In questo blog rappresenta la posizione corrente sulla configurazione delle soluzioni dei partner hello. In tutti i casi, consultare la documentazione della soluzione toopartner prima.
* [Attività e ASC avvisi su syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – questo post di blog viene descritta la procedura hello toosend gli avvisi di attività e Centro sicurezza di Azure su tooQRadar syslog
* [Domande frequenti sull'integrazione dei log di Azure](security-azure-log-integration-faq.md) - Queste domande frequenti riguardano l'integrazione dei log di Azure.
* [L'integrazione di Centro sicurezza PC avvisi con Azure log integrazione](../security-center/security-center-integrating-alerts-with-log-integration.md) : questo documento viene illustrato come centro di sicurezza di Azure toosync avvisi con l'integrazione di Log di Azure.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
