---
title: i dati personali aaaProtect con Centro sicurezza di Azure | Documenti Microsoft
description: Proteggere i dati personali con il Centro sicurezza di Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Proteggere i dati personali da violazioni e attacchi: Centro sicurezza di Azure

In questo articolo consentirà di comprendere la modalità di upera toouse Centro sicurezza di Azure tooprotect dati personali e attacchi.

## <a name="scenario"></a>Scenario 

Una società crociera di grandi dimensioni, sede hello negli Stati Uniti, all'espansione relativo itinerari toooffer operazioni Mediterraneo, hello e mare Baltico, nonché hello isole britannico. toohelp in tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito

la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello. Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito, oltre a informazioni relative alle risorse umane quali:

- Indirizzi
- Numeri di telefono
- Codici fiscali
- Informazioni sanitarie

riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma. Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio hello aziendali presenti in ogni HelloWorld hanno accesso alle risorse aziendali toosome.
Dati personali viaggiano attraverso la rete hello tra questi percorsi e i data center Microsoft hello.

## <a name="problem-statement"></a>Presentazione del problema

la società Hello è interessata sulla minaccia hello di attacchi nelle risorse di Azure. Desiderano tooprevent esposizione delle persone di toounauthorized dati personali dei dipendenti e clienti. Informazioni aggiuntive su sia prevenzione e risposta/monitoraggio e aggiornamento, nonché un modo efficace toomonitor hello in corso la sicurezza delle risorse cloud desiderati.
È necessaria una solida linea di difesa dagli attuali utenti malintenzionati, particolarmente sofisticati e organizzati.

## <a name="company-goal"></a>Obiettivo dell'azienda

Uno degli obiettivi dell'azienda hello è privacy hello tooensure dei dati personali dei dipendenti e clienti per proteggerlo da eventuali minacce. Uno degli obiettivi è toorespond immediatamente toosigns di violazione toomitigate hello impatto. Richiede un modo tooassess hello stato corrente di sicurezza, identificare le configurazioni vulnerabile e aggiornarli.

## <a name="solutions"></a>Soluzioni

Il Centro sicurezza di Microsoft Azure offre una soluzione integrata di monitoraggio della sicurezza e gestione dei criteri. Offre funzionalità efficaci e facili da usare per la prevenzione e il rilevamento delle minacce e la relativa risposta.

### <a name="prevention"></a>Prevenzione

ASC consente di impedire violazioni della sicurezza grazie alla possibilità di criteri di sicurezza tooset, fornire l'accesso a just-in-time e implementare i suggerimenti relativi alla sicurezza.

Un criterio di sicurezza definisce il set di hello dei controlli consigliati per le risorse all'interno di hello specificato sottoscrizione. Solo in fase di accesso può essere utilizzato toolock verso il basso il traffico in entrata tooyour macchine virtuali di Azure, riducendo l'esposizione tooattacks. Consigli relativi alla sicurezza vengono creati da ASC al termine dell'analisi dello stato di sicurezza hello delle risorse di Azure.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Come impostare i criteri di sicurezza nel Centro sicurezza di Azure

È possibile configurare criteri di sicurezza per ogni sottoscrizione. toomodify un criterio di sicurezza, è necessario essere un proprietario o collaboratore della sottoscrizione. Nel portale di Azure hello, hello seguenti:

1. Selezionare **criteri** nel dashboard di hello ASC.

2. Selezionare la sottoscrizione di hello in cui si desidera che i criteri di hello tooenable.

3. Scegliere **criteri di prevenzione** tooconfigure criteri per ogni sottoscrizione. **Raccogliere i dati dalle macchine virtuali** deve essere impostato troppo**in.**

4. In hello **criteri di prevenzione** opzioni, selezionare **su** tooenable hello consigli relativi alla sicurezza riguardano per la sottoscrizione di hello.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Per ulteriori istruzioni e una spiegazione di ognuna delle indicazioni di hello criteri che possono essere abilitate, vedere [impostare criteri di sicurezza nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Come configurare l'accesso Just-in-Time

Quando JIT è abilitato, il Centro sicurezza PC protegge il traffico in entrata tooyour macchine virtuali di Azure creando una regola di gruppo. Selezionare le porte hello in hello VM toowhich verrà bloccato il traffico in ingresso verso il basso. toouse JIT accedere, hello seguenti:

1. Seleziona hello **immediatamente nel riquadro di accesso VM ora** nel pannello ASC hello.

2. Seleziona hello **consigliato** scheda.

3. In **macchine virtuali**, selezionare le macchine virtuali hello che si desidera tooenable. In questo modo un tooa Avanti VM di segno di spunta. 
4. Selezionare **Abilita JIT** in VM.
5. Selezionare **Salva**.

È quindi possibile visualizzare porte predefinite hello che ASC consiglia l'abilitazione per JIT. È anche possibile aggiungere e configurare una nuova porta su cui si desidera hello tooenable solo nella soluzione di tempo. Hello **immediatamente nell'accesso in fase di VM** riquadro nel Centro sicurezza PC hello Mostra il numero di hello di macchine virtuali configurate per l'accesso JIT. Viene inoltre illustrato il numero di hello delle richieste di accesso approvato effettuate in hello ultima settimana.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Per istruzioni su come toodo, e ulteriori informazioni sulla immediatamente accesso ora, vedere [gestire l'accesso alla macchina virtuale con in-time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>Come implementare le raccomandazioni sulla sicurezza del Centro sicurezza di Azure

Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni. indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello necessita. 
1. Seleziona hello **indicazioni** riquadro nel dashboard di hello ASC.

2. Visualizzare le raccomandazioni hello, che vengono visualizzati in un formato di tabella in cui ogni riga rappresenta una raccomandazione.

3. Selezionare toofilter indicazioni, **filtro** e selezionare i valori di gravità e lo stato hello desiderato toosee.

4. toodismiss un'indicazione che non è applicabile, è possibile fare clic destro e selezionare **Elimina.**

5. Valutare la raccomandazione da applicare per prima.

6. Applica indicazioni hello in ordine di priorità.

Per un elenco di possibili indicazioni e procedure su come tooapply ogni, vedere [gestione consigli sulla sicurezza in Centro sicurezza di Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Rilevamento e risposta

Rilevamento e la risposta andare insieme, come si desidera toorespond al più presto dopo che viene rilevata una minaccia.
Rilevamento minacce ASC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso. Il Centro sicurezza di Azure può aggiornare rapidamente gli algoritmi di rilevamento a fronte del rilascio di exploit nuovi e sofisticati da parte di utenti malintenzionati. Per altre informazioni sul funzionamento del rilevamento delle minacce nel Centro sicurezza di Azure, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Come gestire e rispondere toosecurity avvisi?

Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly esaminare il problema di hello. Centro sicurezza PC include inoltre indicazioni sul tooremediate un attacco. toomanage la sicurezza degli avvisi, eseguire hello seguenti:

1. Seleziona hello **degli avvisi di sicurezza** riquadro nel dashboard di hello ASC. Verranno visualizzati i dettagli di ogni avviso.

2. Selezionare gli avvisi toofilter basati sulla data, stato e alla gravità, **filtro** e quindi selezionare i valori hello da toosee.

3. toorespond tooan avviso, selezionarlo e verificare informazioni hello, quindi selezionare hello risorsa che è stato attaccato.

4. In hello **descrizione** campo, si noterà informazioni dettagliate, tra cui monitoraggio e aggiornamento consigliato.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Per informazioni dettagliate sul risponde toosecurity avvisi, vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Per ulteriori informazioni sull'analisi degli avvisi di sicurezza, società hello possibile integrare avvisi ASC con le relative soluzioni SIEM, utilizzando [integrazione di Azure Log](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Come gestire gli eventi imprevisti per la sicurezza

In Centro sicurezza di Azure, un evento imprevisto per la sicurezza è un'aggregazione di tutti gli avvisi relativi a una risorsa corrispondenti a modelli di catena di attacco. Un evento imprevisto riveleranno hello elenco avvisi correlati, che consente di tooobtain ulteriori informazioni su ogni occorrenza. Gli eventi imprevisti vengono visualizzati in hello riquadro avvisi di sicurezza e blade.

tooreview e gestire eventi di sicurezza, hello seguenti:

1. Seleziona hello **degli avvisi di sicurezza** riquadro. Se viene rilevato un problema di sicurezza, viene visualizzato nel grafico gli avvisi di sicurezza hello. con un'icona diversa da quella degli altri avvisi.

2. Selezionare toosee degli eventi imprevisti hello ulteriori dettagli sull'evento imprevisto di sicurezza. Dettagli aggiuntivi includono la descrizione completa, la gravità, il relativo stato corrente, hello attaccata di risorse, i passaggi correttivi hello per evento imprevisto di hello e hello avvisi che sono stati inclusi nell'evento imprevisto.

È possibile filtrare toosee **solo gli eventi imprevisti**, **avvisi solo**, o **entrambi**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>La modalità di accesso di hello Report sullo stato della minaccia

ASC analizza le informazioni da eventuali minacce tooidentify di più origini. i team di risposta agli eventi imprevisti tooassist ricerca e correzione delle minacce, centro di sicurezza include un report sullo stato della minaccia che contiene informazioni sulla minaccia hello che è stato rilevato.

Il Centro sicurezza rende disponibili tre tipi di report per le minacce, che possono variare a seconda dell'attacco.
report di Hello disponibili sono:

- Report sui gruppi di attività: fornisce approfondimenti sugli utenti malintenzionati e relativi obiettivi e strategie.

- Report sulle campagne: si concentra sui dettagli di specifiche campagne di attacco.

- Report di riepilogo minaccia: copre tutti gli elementi di due report hello precedente.

Questo tipo di informazioni è molto utile durante il processo di risposta agli eventi imprevisti hello, in cui è presente un'origine di hello toounderstand analisi in corso di attacco hello, hello motivazioni dell'autore dell'attacco e quali toomitigate toodo questo problema nelle versioni successive.

1. tooaccess hello minacce di report, hello seguenti:

2. Seleziona hello **degli avvisi di sicurezza** riquadro nel dashboard di hello ASC.

3. Selezionare l'avviso di sicurezza hello per cui si desidera tooobtain ulteriori informazioni.

4. In hello **report** campo, fare clic su report sullo stato della minaccia di hello collegamento toohello.

5. Verrà aperto il file PDF hello, che è possibile scaricare.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Per ulteriori informazioni su hello report sullo stato della minaccia ASC, vedere [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Valutazione

toohelp con test e valutare le condizioni di sicurezza, ASC fornisce per la valutazione delle vulnerabilità integrata con Qualys agenti cloud, come parte del componente indicazioni macchina virtuale.

agente Qualys Hello report vulnerabilità dati toohello Qualys piattaforma di gestione, che quindi invia la vulnerabilità e dei dati di monitoraggio dell'integrità, eseguire il backup tooASC. Hello tooadd indicazione viene visualizzata una soluzione per la valutazione delle vulnerabilità in hello **indicazioni** pannello nel dashboard di hello ASC.

Dopo l'installazione di soluzioni di valutazione delle vulnerabilità hello destinazione hello VM, analisi di Centro sicurezza PC hello toodetect VM e identificano le vulnerabilità di sistema e dell'applicazione. Rilevati problemi vengono visualizzati sotto hello **indicazioni di macchine virtuali** opzione.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Come implementare una soluzione di valutazione della vulnerabilità 

Se in una macchina virtuale non è già distribuita una soluzione di valutazione della vulnerabilità, il Centro sicurezza ne raccomanda l'installazione.

1. Nel dashboard ASC hello in hello **indicazioni** pannello seleziona **aggiungere una soluzione per la valutazione delle vulnerabilità.**

2. Selezionare le macchine virtuali hello in cui si desidera soluzione per la valutazione delle vulnerabilità tooinstall hello.

3. Fare clic su **Installa su [numero di] VM.**

4. Selezionare una soluzione di partner in hello Azure Marketplace o under **usare una soluzione esistente,** selezionare **Qualys.**

5. È possibile attivare le impostazioni di aggiornamento automatico hello o disattivare in hello **soluzioni dei Partner** blade.

Per ulteriori informazioni su come tooimplement una soluzione per la valutazione delle vulnerabilità, vedere [valutazione delle vulnerabilità nel Centro protezione di Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Passaggi successivi

- [Guida introduttiva per il Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Introduzione tooAzure Centro sicurezza](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Integrazione degli avvisi del Centro sicurezza di Azure con l'integrazione dei log di Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Ottimizzare il Centro sicurezza di Azure con la valutazione integrata della vulnerabilità](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
