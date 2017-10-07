---
title: aaaMonitoring e risposta tooSecurity avvisi in Operations Management Suite di protezione e controllo soluzione | Documenti Microsoft
description: Questo documento consente si toouse hello threat intelligence opzione disponibile in OMS sicurezza e controllo toomonitor e risposta toosecurity avvisi.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>Monitorare e rispondere toosecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite
Questo documento consente di utilizzare hello threat intelligence opzione disponibile in OMS sicurezza e controllo toomonitor e rispondere toosecurity avvisi.

## <a name="what-is-oms"></a>Cos'è OMS?
Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Per ulteriori informazioni su OMS, leggere l'articolo hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="threat-intelligence"></a>Intelligence per le minacce
In un ambiente aziendale in cui gli utenti accesso ampio toohello rete e utilizzano una varietà di dispositivi tooconnect toocorporate dati, è fondamentale che è possibile monitorare attivamente le risorse e rispondere rapidamente gli eventi imprevisti toosecurity. Questo è particolarmente importante dalla prospettiva del ciclo di vita di sicurezza hello perché alcuni riguardanti la sicurezza minacce potrebbero non generare avvisi o le attività sospette che possono essere identificate tramite controlli tecnici di sicurezza tradizionali. 

Utilizzando hello **minacce** opzione disponibili in OMS Security and Audit, gli amministratori IT può identificare i rischi di sicurezza ambiente hello, ad esempio, identificare se un determinato computer fa parte di un [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection). I computer possono diventare i nodi in una botnet quando gli utenti malintenzionati illecitamente installa il software dannoso che si connette segretamente questo comando toohello computer e il controllo. Questa funzionalità è anche in grado di identificare potenziali minacce provenienti da canali di comunicazione sotterranei, ad esempio una [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents). 

In ordine toobuild sulle minacce, OMS Security and Audit utilizzare dati provenienti da più origini all'interno di Microsoft. OMS Security and Audit sfruttano questa tooidentify potenziali minacce per i dati contro l'ambiente.

riquadro di informazioni sulle minacce Hello è composto da tre principali opzioni:

* Server con traffico dannoso in uscita
* Tipi di minacce rilevate
* Mappa di intelligence per le minacce

> [!NOTE]
> Per una panoramica di tutte queste opzioni, leggere [Introduzione alla soluzione Sicurezza e controllo di Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="responding-toosecurity-alerts"></a>Risponde toosecurity avvisi
Uno dei passaggi di hello di un [risposta agli eventi imprevisti di protezione](https://technet.microsoft.com/library/cc512623.aspx) processo è il livello di gravità di tooidentify hello del sistema di compromissione hello. In questa fase è necessario eseguire hello seguenti attività:

* Determinare la natura hello di attacco hello
* Determinare il punto di attacco hello di origine.
* Determinare l'intento di hello di attacco hello. È stato casuale o è stato espressamente le informazioni specifiche di organizzazione tooacquire attacco di hello?
* Identificare i sistemi di hello che sono stato compromesso
* Identificare i file hello che sono stati eseguiti e determinano la sensibilità hello di tali file

È possibile sfruttare **minacce** informazioni in OMS Security and Audit toohelp soluzione con queste attività. Seguire i passaggi di hello sotto tooaccess **minacce** opzioni:

1. In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **Security and Audit** riquadro.
   
    ![Security and Audit](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. In hello **Security and Audit** dashboard, si noterà hello **minacce** opzioni nella finestra di destra hello, come illustrato di seguito:
   
    ![Intelligence per le minacce](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

Questi tre riquadri offrono una panoramica delle minacce corrente hello. In hello **Server con traffico dannoso in uscita** sarà in grado di tooidentify se esiste qualsiasi computer che si sta monitorando (all'interno o all'esterno della rete) vale a dire toohello traffico dannoso invio Internet. 

Hello **rilevati tipi di minacce** riquadro viene visualizzato un riepilogo delle minacce hello correnti "in hello wild", se si fa clic su questo riquadro verranno visualizzati ulteriori dettagli su queste minacce come illustrato di seguito:

![Tipi di minacce rilevate](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

È possibile ottenere altre informazioni facendo clic su ogni minaccia. esempio Hello riportato di seguito mostra ulteriori dettagli su Botnet:

![altri dettagli su una minaccia](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

Come descritto in questa sezione di inizio hello, queste informazioni possono essere molto utile durante un caso di risposta agli eventi imprevisti. Può anche essere importante durante un'analisi forense, in cui è necessario origine hello toofind attacco hello, il sistema è stato compromesso e hello sequenza temporale. In questo report è possibile identificare facilmente alcuni dettagli chiave sull'attacco hello, ad esempio: hello origine dell'attacco hello, hello IP locale che è stata compromessa e lo stato della sessione corrente della connessione hello hello. 

Hello **mappa intelligence minaccia** consentirà di tooidentify hello corrente le località in tutto il mondo hello con traffico dannoso. Sono disponibili arancione (in entrata) e (in uscita) frecce rosse in questa mappa che identificano direzione del traffico di hello, se fa clic su una di queste frecce, verrà visualizzato il tipo di hello della direzione del traffico di minacce e hello come illustrato di seguito:

![mappa di intelligence per le minacce](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> È possibile visualizzare una dimostrazione sul toouse questa funzionalità durante un intervento sul processo, è possibile guardare la presentazione hello [ridurre i rischi di protezione di datacenter con ricerca interattiva tramite Operations Management Suite](https://myignite.microsoft.com/videos/5000) recapitare in Microsoft Ignite.
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>Risponde toodistinct IP dannosi accedere
In alcuni scenari è possibile notare un potenziale IP dannoso a cui è stato eseguito l'accesso da un computer monitorato:

![mappa di intelligence per le minacce](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Questo avviso e altri utenti all'interno di hello stessa categoria, vengono generati tramite la sicurezza di OMS sfruttando [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). dati sulle minacce Hello è raccolti da Microsoft, nonché acquistata da provider leader nei threat intelligence. Questi dati vengono modificati di frequente e adattare lo spostamento toofast minacce. A causa di natura tooits, deve essere combinato con altre fonti di informazioni di sicurezza durante [analizzando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) un avviso di sicurezza. 

## <a name="customize-alerts-received-via-e-mail"></a>Personalizzare gli avvisi ricevuti tramite posta elettronica

È possibile personalizzare gli utenti nell'organizzazione che riceveranno una notifica quando vengono attivati gli avvisi di sicurezza dalla sicurezza di OMS. Questa opzione è disponibile in panoramica / dashboard OMS di hello impostazioni:

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso hello toouse **minacce** opzione negli avvisi di toosecurity toorespond soluzioni OMS Security and Audit. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Introduzione alla soluzione Sicurezza e controllo di Operations Management Suite](oms-security-getting-started.md)
* [Monitoraggio delle risorse nella soluzione Sicurezza e controllo di Operations Management Suite](oms-security-monitoring-resources.md)

