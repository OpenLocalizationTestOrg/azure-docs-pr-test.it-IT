---
title: aaaGetting avviato con soluzione di controllo e protezione di Operations Management Suite | Documenti Microsoft
description: "Consente di questo documento si tooget avviato con Operations Management Suite Security and Audit toomonitor funzionalità soluzione cloud ibrido."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Introduzione alla soluzione Sicurezza e controllo di Operations Management Suite
Questo documento consente di iniziare rapidamente a usare le funzionalità della soluzione Sicurezza e controllo di Operations Management Suite (OMS), illustrando ogni opzione.

## <a name="what-is-oms"></a>Cos'è OMS?
Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Per ulteriori informazioni su OMS, leggere l'articolo hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Dashboard di Sicurezza e controllo di OMS
soluzioni OMS Security and Audit Hello fornisce un quadro completo dell'organizzazione condizioni di sicurezza IT con query di ricerca predefinite relative a problemi rilevanti che richiedono attenzione. Hello **Security and Audit** dashboard è schermata iniziale di hello per tutti gli elementi correlati toosecurity in OMS. Fornisce ad alto livello comprendere hello stato di protezione dei computer. Include inoltre hello possibilità tooview tutti gli eventi da hello ultime 24 ore, 7 giorni, o qualsiasi altro intervallo di tempo personalizzato. hello tooaccess **Security and Audit** dashboard, eseguire la procedura seguente:

1. In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **impostazioni** riquadro a sinistra di hello.
2. In hello **impostazioni** pannello, in **soluzioni** fare clic su **Security and Audit** opzione.
3. Hello **Security and Audit** verrà visualizzato il dashboard:
   
    ![Dashboard di Sicurezza e controllo di OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Se si accede a questo dashboard per hello prima volta e non si dispone di dispositivi monitorati da OMS, hello riquadri non vengano inseriti dati ottenuti dall'agente hello. Dopo aver installato l'agente di hello, possono essere necessari alcuni toopopulate tempo, pertanto ciò che viene visualizzato inizialmente potrebbe mancare alcuni dati come sono ancora in corso il caricamento toohello cloud.  In questo caso, è normale toosee alcuni riquadri senza informazioni tangibili. Lettura [connettere i computer Windows direttamente tooOMS](https://technet.microsoft.com/library/mt484108.aspx) per ulteriori informazioni sull'agente OMS tooinstall in un sistema di Windows e [tooOMS computer Linux di connettersi](https://technet.microsoft.com/library/mt622052.aspx) per ulteriori informazioni su come tooperform questa attività in un sistema Linux.

> [!NOTE]
> agente Hello raccoglie le informazioni di hello in base a hello corrente eventi che sono abilitati, ad esempio nome del computer, nome utente e all'indirizzo IP. Non vengono tuttavia raccolti documenti o file, nomi del database o dati personali.   
> 
> 

Le soluzioni sono una raccolta di regole di logica, visualizzazione e acquisizione dei dati che permettono di risolvere le principali problematiche dei clienti. Sicurezza e controllo è una soluzione, altre possono essere aggiunte separatamente. Leggere l'articolo hello [aggiungere soluzioni](https://technet.microsoft.com/library/mt674635.aspx) per ulteriori informazioni su come tooadd una nuova soluzione.

dashboard di OMS Security and Audit Hello è organizzata in quattro categorie principali:

* **Domini di sicurezza**: in quest'area sarà toofurther in grado di esplorare i record di sicurezza nel tempo, accedere alla valutazione del malware, aggiornare valutazione, la protezione della rete, le informazioni di identità e accessi, i computer con gli eventi di sicurezza e rapidamente dashboard di Centro sicurezza PC tooAzure di accesso.
* **Problemi rilevanti**: questa opzione consentirà tooquickly identificare il numero di problemi attivi hello e hello gravità di questi problemi.
* **Rilevamenti (anteprima)**: consente di schemi di attacco tooidentify visualizzando gli avvisi di sicurezza come che si verificano rispetto alle risorse.
* **Minaccia Intelligence**: consente di schemi di attacco tooidentify, visualizzazione del numero totale di hello del server con traffico IP dannoso in uscita, il tipo di minaccia intenzionale hello e una mappa che mostra provenienza questi indirizzi IP. 
* **Query comuni di sicurezza**: questa opzione offre è un elenco di sicurezza più comune di hello esegue una query che è possibile utilizzare toomonitor l'ambiente. Quando si fa clic in uno di tali query, aprirla hello **ricerca** pannello con risultati hello per tale query.

> [!NOTE]
> Per altre informazioni sulla modalità di protezione dei dati in OMS, vedere l'articolo che illustra come OMS protegge i dati.
> 
> 

## <a name="security-domains"></a>Domini di sicurezza
Durante il monitoraggio delle risorse, è importante toobe tooquickly in grado di accedere hello stato corrente dell'ambiente. Tuttavia è anche importante toobe tootrack in grado di back-gli eventi generati in hello precedente che possono portare tooa una migliore comprensione di ciò che avviene nell'ambiente in uso in determinato punto nel tempo. 

> [!NOTE]
> conservazione dei dati viene eseguito in base toohello piano dei prezzi di OMS. Per ulteriori informazioni visitare hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) pagina dei prezzi.
> 
> 

Scenari di analisi forense e risposta degli eventi imprevisti trarranno vantaggio direttamente dai risultati di hello disponibili in hello **i record di sicurezza nel tempo** riquadro.

![Record di sicurezza nel tempo](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Quando si fa clic su questo riquadro, hello **ricerca** pannello verrà aperto, che mostra il risultato di una query per **gli eventi di sicurezza** (tipo = SecurityEvents) con dati in base hello negli ultimi sette giorni, come illustrato di seguito:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Record di sicurezza nel tempo](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

risultato della ricerca Hello è suddivisa in due riquadri: riquadro di sinistra hello fornisce una descrizione dettagliata del numero di hello degli eventi di sicurezza che sono stati trovati computer hello in cui questi eventi sono stati trovati, hello numero di account che sono stati individuati in tali computer e i tipi di hello di attività. riquadro di destra Hello fornisce risultati totali hello e una visualizzazione cronologica hello degli eventi di sicurezza con attività di nome e all'evento del computer hello. È anche possibile fare clic su **Mostra altre** tooview informazioni più dettagliate su questo evento, ad esempio dati dell'evento hello, ID evento hello e origine evento hello.

> [!NOTE]
> Per altre informazioni sulle query di ricerca di OMS, vedere [Informazioni di riferimento sulla ricerca in OMS](https://technet.microsoft.com/library/mt450427.aspx).
> 
> 

### <a name="antimalware-assessment"></a>Antimalware Assessment
In questo modo opzione tooquickly è identificare i computer con protezione insufficiente e i computer che sono compromesso da una parte del malware. Malware assessment stato potenziali minacce per server hello monitorato vengono lette e hello quindi i dati vengono inviati servizio OMS toohello in cloud hello per l'elaborazione. I server con minacce attive e protezione insufficiente vengono visualizzati nel dashboard di valutazione di hello malware, è possibile accedere dopo aver fatto clic in hello **Antimalware Assessment** riquadro. 

![Valutazione malware](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Analogamente alle altre riquadro animato disponibili nel Dashboard di OMS, quando si fa clic su di esso, hello **ricerca** pannello verrà aperto con i risultati della query hello. Per questa opzione, se si fa clic in hello **non Reporting** opzione **lo stato di protezione**, si disporrà di risultato della query hello che illustra questa voce singola che contiene il nome del computer hello e la relativa classificazione, di seguito riportato:

![Risultato della ricerca](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *numero di dimensioni* è un livello che lo stato di hello tooreflect di protezione hello (on, off, aggiornato, e così via) e minacce disponibili. Visto che come un numero aggregazioni toomake consente.
> 
> 

Se si fa clic nel nome del computer hello, sarà necessario vista cronologico di hello dello stato di protezione hello per questo computer. È molto utile per scenari in cui è necessario toounderstand se hello antimalware era installato e a un certo punto è stato rimosso.   

### <a name="update-assessment"></a>Valutazione aggiornamenti
Abilita questa opzione è tooquickly determinare hello problemi di sicurezza toopotential esposizione globale, se e o l'importanza con cui questi aggiornamenti sono per l'ambiente. Soluzione di controllo e sicurezza OMS forniscono solo visualizzazione hello di questi aggiornamenti, hello reale dati provengono da [soluzioni](oms-solution-update-management.md), ovvero un modulo diverso all'interno di OMS. Ecco un esempio degli aggiornamenti di hello:

![Aggiornamenti di sistema](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Per altre informazioni sulla soluzione Gestione aggiornamenti, vedere [Soluzione Gestione aggiornamenti in OMS](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Identità e accesso
Identità deve essere controllo hello piano per l'organizzazione, protezione dell'identità deve essere la priorità superiore. Mentre nelle ultime hello sono presenti perimetro intorno alle organizzazioni e tali perimetro è uno dei limiti difensivo primario hello, oggi con più dati e altre App mobile toohello cloud identity hello diventa perimetrale nuovo hello. 

> [!NOTE]
> attualmente dati hello sono basati solo su dati di accesso di eventi di sicurezza (evento ID 4624) nell'account di accesso di hello future Office 365 e dati di Azure AD verranno inoltre inclusi.
> 
> 

Monitorando le attività di identity sarà azioni proattive tootake in grado di rendere sul posto o azioni reattivo toostop un tentativo di attacco di un evento imprevisto. Hello **identità e accessi** dashboard fornisce una panoramica dello stato di identità, tra cui hello numero di tentativi non riusciti toolog on, hello account utente che sono stati utilizzati durante i tentativi, gli account che sono stati bloccati, gli account con modificare o reimpostare la password ed è attualmente il numero di account che vengono registrati nel. 

Quando si sceglie hello **identità e accessi** riquadro verrà visualizzato hello seguente dashboard:

![Identità e accesso](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

informazioni di Hello disponibili in questo dashboard possono essere immediatamente utili si tooidentify potenziale di un'attività sospetta. Ad esempio, vi sono 338 toolog tentativi in come **amministratore** e 100% di questi tentativi non riusciti. Questo può essere dovuto a un attacco di forza bruta verso questo account. Se fa clic su questo account si ottengono informazioni che possono facilitare la risorsa di destinazione hello toodetermine per questo tipo di attacco potenziale:

![risultati della ricerca](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

report dettagliato Hello fornisce importanti informazioni sull'evento, tra cui: i computer di destinazione hello, tipo di hello di accesso (in questo caso accesso alla rete), l'attività hello (in questo caso evento 4625) e una cronologia completa di ogni tentativo. 

### <a name="computers"></a>Computer
Questo riquadro può essere utilizzato tooaccess tutti i computer con attivamente gli eventi di sicurezza. Quando si fa clic in questa sezione verrà visualizzato hello elenco di computer con eventi di sicurezza e il numero di hello di eventi in ogni computer:

![Computer](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

È possibile continuare l'analisi facendo clic su ogni computer e rivedere gli eventi di sicurezza hello che sono stati contrassegnati.

### <a name="threat-intelligence"></a>Intelligence per le minacce

L'opzione hello minacce disponibili in OMS Security and Audit, gli amministratori IT può identificare i rischi di sicurezza ambiente hello, ad esempio, identificare se un determinato computer fa parte di una botnet. I computer possono diventare i nodi in una botnet quando gli utenti malintenzionati illecitamente installa il software dannoso che si connette segretamente questo comando toohello computer e il controllo. Questa funzionalità può anche identificare potenziali minacce provenienti da canali di comunicazione sotterranei, ad esempio una darknet. Per ulteriori informazioni sulle minacce, la lettura [toosecurity monitoraggio e che risponda gli avvisi in Operations Management Suite di protezione e controllo soluzione](oms-security-responding-alerts.md) articolo.

In alcuni scenari è possibile notare un potenziale IP dannoso a cui è stato eseguito l'accesso da un computer monitorato:

![mappa di intelligence per le minacce](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Questo avviso e altri utenti all'interno di hello stessa categoria, vengono generati tramite la sicurezza di OMS sfruttando [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8). dati sulle minacce Hello è raccolti da Microsoft, nonché acquistata da provider leader nei threat intelligence. Questi dati vengono modificati di frequente e adattare lo spostamento toofast minacce. A causa di natura tooits, deve essere combinato con altre fonti di informazioni di sicurezza durante [analizzando](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) un avviso di sicurezza. 

### <a name="baseline-assessment"></a>Valutazione di base

Microsoft, insieme ad altre organizzazioni del settore e governative in tutto il mondo, definisce una configurazione di Windows che rappresenta distribuzioni server a sicurezza elevata. Questa configurazione è un set di chiavi del Registro di sistema, impostazioni dei criteri di controllo e impostazioni di criteri di sicurezza, oltre ai valori consigliati di Microsoft per queste impostazioni. Questo set di regole è noto come baseline sicurezza. Vedere [Valutazione baseline nella soluzione Sicurezza e controllo di Operations Management Suite](oms-security-baseline.md) per altre informazioni su questa opzione.

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Questo riquadro è fondamentalmente un dashboard di scelta rapida tooaccess Centro sicurezza di Azure. Per altre informazioni su questa soluzione, vedere [Introduzione al Centro sicurezza Azure](../security-center/security-center-get-started.md) .

## <a name="notable-issues"></a>Errori rilevanti
scopo principale di Hello di questo gruppo di opzioni è tooprovide una visualizzazione rapida dei problemi di hello presenti nel proprio ambiente, suddividendoli in critico, avviso e informativi. Hello riquadro di tipo di problema attivo è una visualizzazione di questi problemi, ma non consente più dettagli su di essi, tooexplore per cui occorre parte inferiore di hello toouse di questo riquadro che contiene il nome di hello del problema hello (nome), il numero di oggetti ha questo verificarsi (conteggio) e l'importanza è (GRAVITÀ).

![Errori rilevanti](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

È possibile vedere che questi problemi sono stati già analizzati in diverse aree di hello **domini di sicurezza** gruppo che rafforza finalità hello di questa vista: visualizzare i problemi più importanti di hello nell'ambiente in uso da un'unica posizione.

## <a name="detections-preview"></a>Rilevamenti (anteprima)
scopo principale di questa opzione Hello è tooallow IT tooquickly identificare potenziali minacce tootheir ambiente di tramite e gravità hello di questa minaccia.

![Intelligence per le minacce](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Questa opzione può anche essere utilizzata durante un [analisi risposta agli eventi imprevisti](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform hello assessment e ottenere ulteriori informazioni su attacco hello.

> [!NOTE]
> Per ulteriori informazioni su come toouse OMS per l'evento imprevisto di risposta, guardare questo video: [come tooLeverage hello Centro sicurezza di Azure & Microsoft Operations Management Suite per una risposta a eventi imprevisti](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Intelligence per le minacce
Hello minaccia nuova sezione di business intelligence della soluzione Security and Audit hello Visualizza gli schemi di attacco possibili hello in diversi modi: hello numero totale di server con traffico IP dannoso in uscita, hello tipo dannoso minaccia e una mappa in cui viene illustrato dove questi indirizzi IP provenienti da. È possibile interagire con mappa di hello e fare clic su hello gli indirizzi IP per altre informazioni.

Gialli puntine da disegno nella mappa hello indicano il traffico in ingresso da indirizzi IP dannosi. Non è insolito per i server che sono esposte traffico dannoso in ingresso toosee toohello internet, ma si consiglia di esaminare questi tentativi toomake che nessuno di essi ha avuto esito positivo. Questi indicatori sono basati sui log di IIS, WireData e i registri di Windows Firewall.  

![Intelligence per le minacce](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Query comuni sulla sicurezza
elenco di Hello di query comuni di sicurezza disponibili possa essere utili per le informazioni si toorapidly accesso della risorsa e personalizzarlo in base alle esigenze dell'ambiente. Queste query comuni sono:

* Tutte le attività di sicurezza
* Attività di sicurezza nel computer "computer01.contoso.com" (sostituire con il nome computer desiderato) hello
* Attività di sicurezza nel computer "computer01.contoso.com hello" per l'account "Administrator" (sostituire con i propri nomi computer e account)
* Attività di accesso per computer
* Account che hanno terminato il servizio Microsoft Antimalware in qualsiasi computer
* Computer in cui è stato terminato hello processo Microsoft antimalware
* Computer in cui è stato eseguito il processo "hash.exe" (sostituire con il nome di processo desiderato)
* Tutti i nomi dei processi eseguiti
* Attività di accesso per account
* Account che ha eseguito in modalità remota sul computer "computer01.contoso.com" (sostituire con il nome computer desiderato) hello

## <a name="see-also"></a>Vedere anche
In questo documento, sono state introdotte tooOMS soluzione Security and Audit. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

