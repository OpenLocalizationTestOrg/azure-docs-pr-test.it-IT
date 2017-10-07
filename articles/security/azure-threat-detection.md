---
title: aaaAzure avanzate di rilevamento minacce | Documenti Microsoft
description: "Informazioni sulla protezione delle identità e le relative funzionalità."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Rilevamento delle minacce avanzato in Azure
## <a name="introduction"></a>Introduzione

### <a name="overview"></a>Panoramica

Microsoft ha sviluppato una serie di White paper, sicurezza panoramiche, procedure consigliate e gli elenchi di controllo tooassist Azure clienti riguardo hello varie funzionalità correlate alla sicurezza disponibili in e hello circostante piattaforma Azure. intervallo di argomenti in termini di dimensioni e della complessità Hello e vengono aggiornate periodicamente. Questo documento fa parte della serie, come riepilogato nella seguente sezione astratta hello.

### <a name="azure-platform"></a>Piattaforma Azure

Azure è una piattaforma cloud pubblico del servizio che supporta hello selezione più ampia di sistemi operativi, linguaggi di programmazione, Framework, strumenti, i database e i dispositivi.
Supporta i seguenti linguaggi di programmazione hello:
-   Eseguire i contenitori Linux con l'integrazione Docker.
-   Compilare le app con JavaScript, Python, .NET, PHP, Java e Node.js.
-   Compilare back-end per dispositivi iOS, Android e Windows.

Servizi cloud pubblico di Azure supportano hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si esegue la migrazione tooa cloud pubblico con un'organizzazione, questa organizzazione è tooprotect responsabile dei dati e fornire una protezione e governance intorno sistema hello.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende grado di soddisfare le esigenze di sicurezza. Azure offre un'ampia gamma di opzioni tooconfigure e personalizzare i requisiti di sicurezza toomeet hello delle distribuzioni di app. Questo documento consente di soddisfare questi requisiti.

### <a name="abstract"></a>Sunto

Microsoft Azure offre funzionalità predefinite di rilevamento delle minacce avanzato attraverso servizi quali Azure Active Directory, Azure Operations Management Suite (OMS) e Centro sicurezza di Azure. Questa raccolta di funzionalità e i servizi di sicurezza fornisce toounderstand un modo semplice e rapido cosa avviene all'interno di distribuzioni di Azure.

Questo white paper guiderà l'utente hello "Microsoft Azure approcci" verso vulnerabilità minaccia diagnostica e analisi dei rischi hello associati con le attività dannose di hello assegnate in base al server e altre risorse di Azure. In questo modo è tooidentify hello metodi di identificazione e gestione delle vulnerabilità con con ottimizzazione per la soluzione hello piattaforma Azure e servizi di sicurezza che riguardano il cliente e le tecnologie.

Questo white paper è incentrato sulla tecnologia hello della piattaforma Azure e i controlli che riguardano il cliente e non tooaddress i contratti di servizio, i modelli dei prezzi e considerazioni sulle procedure consigliate di DevOps.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) è una funzionalità di hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition che fornisce una panoramica degli eventi di rischio hello e potenziali vulnerabilità che interessano l'organizzazione identità. Microsoft è stato protezione identità basate su cloud per oltre un decennio e con Azure AD Identity Protection, Microsoft sta questi stessi sistemi di protezione disponibili tooenterprise clienti. Identity Protection si avvale delle funzionalità di rilevamento anomalie di Azure AD, disponibili tramite i [report di Anomalie dell'attività di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports), e introduce nuovi tipi di eventi di rischio che permettono di rilevare le anomalie in tempo reale.

La protezione dell'identità utilizza algoritmi di apprendimento automatico adattivo e anomalie toodetect euristica e gli eventi di rischio che potrebbero indicare che un'identità sia stato compromesso. Con questi dati, la protezione dell'identità genera i report e avvisi che consentono di tooinvestigate questi eventi di rischio e intraprendere l'azione di correzione o riduzione appropriata.

Azure Active Directory Identity Protection è, del resto, ben più di un semplice strumento di monitoraggio e reporting. Basato su eventi di rischio, la protezione dell'identità calcola un livello di rischio utente per ogni utente, consentendo di criteri basati sul rischio tooconfigure tooautomatically proteggere hello identità dell'organizzazione.

Questi criteri basati sui rischi, in aggiunta tooother [i controlli di accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) forniti da Azure Active Directory e [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), automaticamente possono bloccare o offrono le azioni di correzione adattivo che includono la reimpostazione della password e l'applicazione multi-factor authentication.

### <a name="identity-protections-capabilities"></a>Funzionalità di Identity Protection

Azure Active Directory Identity Protection è ben più di un semplice strumento di monitoraggio e reporting. tooprotect identità dell'organizzazione, è possibile configurare criteri basati sui rischi di rispondere automaticamente toodetected problemi quando viene raggiunto un livello di rischio specificato. Questi criteri, inoltre tooother condizionale accedere ai controlli forniti da Azure Active Directory ed EMS, può bloccare automaticamente oppure avviare azioni di correzione adattivo inclusi la reimpostazione della password e l'applicazione multi-factor authentication.

Esempi di alcuni dei modi hello che la protezione dell'identità di Azure consentono di proteggere gli account e le identità includono:

[Rilevamento di eventi di rischio e account rischiosi:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Rilevamento di sei tipi di eventi di rischio tramite regole euristiche e apprendimento automatico.
-   Calcolo dei livelli di rischio utente.
-   Fornire consigli personalizzati tooimprove generali di sicurezza, evidenziando le vulnerabilità

[Analisi degli eventi di rischio:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Invio di notifiche per gli eventi di rischio.
-   Analisi degli eventi di rischio con informazioni rilevanti e contestuali.
-   Fornisce i flussi di lavoro di base indagini tootrack
-   Fornendo un accesso semplice tooremediation azioni, ad esempio la reimpostazione della password

[Criteri di accesso condizionale basati sul rischio:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Criteri toomitigate rischiosi accessi da accessi di blocco o la richiesta di richieste di autenticazione a più fattori.
-   Criteri tooblock o gli account utente di rischiosa sicura
-   Criteri toorequire utenti tooregister multi-factor Authentication

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

Con [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Gestione identità con privilegi di Azure AD](./media/azure-threat-detection/azure-threat-detection-fig2.png)

è possibile gestire, controllare e monitorare l'accesso all'interno dell'organizzazione. Ciò include tooresources di accesso di Azure AD e altri Microsoft online services quali Office 365 o Microsoft Intune.

Azure AD Privileged Identity Management consente di effettuare le operazioni seguenti:

-   Ricevere un avviso e di segnalare gli amministratori di Azure AD e "just in time" accesso amministrativo tooMicrosoft Online Services quali Office 365 e Intune

-   Ottenere report sulla cronologia degli accessi degli amministratori e sulle modifiche alle assegnazioni degli amministratori

-   Ottenere avvisi relativi al ruolo con privilegi di accesso tooa

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Poiché OMS viene implementato come servizio basato sul cloud, è possibile renderlo operativo rapidamente con un investimento minimo nei servizi di infrastruttura. Le nuove funzionalità di sicurezza sono disponibili automaticamente, evitando così i costi di manutenzione e aggiornamento continui.

È inoltre possono integrare tooproviding importanti servizi nel proprio OMS con componenti di System Center, ad esempio [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend protezione gestione investimenti esistenti in hello cloud. System Center e OMS possono essere usati insieme tooprovide esperienza di una gestione ibrida completa.

### <a name="holistic-security-and-compliance-posture"></a>Approccio olistico a sicurezza e conformità

Hello [dashboard OMS Security and Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fornisce un quadro completo dell'organizzazione condizioni di sicurezza IT con query di ricerca predefinite relative a problemi rilevanti che richiedono attenzione. dashboard di sicurezza e controllo Hello è schermata iniziale di hello per tutti gli elementi correlati toosecurity in OMS. Fornisce ad alto livello comprendere hello stato di protezione dei computer. Include inoltre hello possibilità tooview tutti gli eventi da hello ultime 24 ore, 7 giorni, o qualsiasi altro intervallo di tempo personalizzato.

Consente di dashboard OMS di comprendere rapidamente e facilmente hello generali di sicurezza di un ambiente, tutti nel contesto di hello delle operazioni IT, tra cui: valutazione di aggiornamento software antimalware assessment e linee di base di configurazione. Inoltre, sono facilmente accessibili i dati del Registro di sicurezza toostreamline hello sicurezza e conformità dei processi di controllo.

dashboard di OMS Security and Audit Hello è organizzata in quattro categorie principali:

![Dashboard di Sicurezza e controllo di OMS](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Domini di sicurezza:** in questa area, si sarà in grado di toofurther esplorare i record di sicurezza nel tempo, accedere alla valutazione del malware, aggiornare valutazione, la protezione della rete, le informazioni di identità e accessi, i computer con gli eventi di sicurezza e rapidamente dashboard di Centro sicurezza PC tooAzure di accesso.

-   **Problemi rilevanti:** questa opzione consente di tooquickly identificare il numero di problemi attivi hello e hello gravità di questi problemi.

-   **Rilevamenti (anteprima):** consente schemi di attacco tooidentify visualizzando gli avvisi di sicurezza come che si verificano rispetto alle risorse.

-   **Informazioni sulle minacce:** consente schemi di attacco tooidentify dalla visualizzazione del numero totale di hello del server con traffico IP dannoso in uscita, il tipo di minaccia intenzionale hello e una mappa che mostra provenienza questi indirizzi IP.

-   **Query comuni di sicurezza:** questa opzione offre è un elenco di sicurezza più comune di hello esegue una query che è possibile utilizzare toomonitor l'ambiente. Quando si fa clic in uno di tali query, viene aperto il pannello di ricerca hello con risultati hello per tale query.

### <a name="insight-and-analytics"></a>Insight & Analytics
Nella parte centrale della hello [Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) è il repository OMS hello, che è ospitato in hello cloud di Azure.

![Insight & Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Raccolta dei dati nel repository di hello dai origini connesse, la configurazione delle origini dati e Aggiunta sottoscrizione tooyour di soluzioni.

![sottoscrizione](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Origini dati e soluzioni ogni creare tipi di record diversi possono ancora essere analizzati insieme nel repository di query toohello ma il proprio set di proprietà. In questo modo hello toouse stesso toowork strumenti e i metodi con diversi tipi di dati raccolti da diverse origini.


La maggior parte dell'interazione con i Log Analitica è tramite il portale OMS hello, che viene eseguita in qualsiasi browser e fornisce le impostazioni di accesso tooconfiguration e più strumenti tooanalyze e agire sui dati raccolti. Dal portale di hello, è possibile utilizzare [log ricerche](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) in cui si creano query tooanalyze raccolti dati, [dashboard](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), che è possibile personalizzare i grafici di ricerche utili e [soluzioni](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), che forniscono gli strumenti di analisi e funzionalità aggiuntivi.

![strumenti di analisi](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Le soluzioni aggiungono funzionalità tooLog Analitica. Sono principalmente eseguiti nel cloud hello e fornire un'analisi dei dati raccolti nel repository OMS hello. Possono anche definire raccolti nuovo toobe tipi di record che può essere analizzati con ricerche nei Log o tramite l'interfaccia utente aggiuntive fornite dalla soluzione hello nel dashboard OMS hello.
Hello Security and Audit è riportato un esempio di questi tipi di soluzioni.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automazione e controllo: avvisi di deviazione dalla configurazione di sicurezza

Automazione di Azure automatizza i processi amministrativi con i runbook che sono basati su PowerShell ed eseguiti nel cloud di Azure hello. I runbook possono inoltre essere eseguiti in un server delle risorse locali di center toomanage dati locali. Automazione di Azure consente la gestione della configurazione con PowerShell DSC (Desired State Configuration).

![Automazione di Azure](./media/azure-threat-detection/azure-threat-detection-fig7.png)

È possibile creare e gestire risorse DSC ospitate in Azure e applicarle toodefine sistemi locali e toocloud e automaticamente applicare loro configurazione o ottenere i report in caso di deviazione toohelp assicurare che le configurazioni di sicurezza rimangono all'interno dei criteri.

## <a name="azure-security-center"></a>Centro sicurezza di Azure

Il Centro sicurezza di Azure consente di proteggere le risorse di Azure. Integra il monitoraggio della sicurezza e la gestione dei criteri in tutte le sottoscrizioni di Azure. All'interno del servizio di hello, si è in grado di toodefine criteri non solo per le sottoscrizioni di Azure, ma anche contro [gruppi di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), in modo da essere più granulare.

![Centro sicurezza di Azure](./media/azure-threat-detection/azure-threat-detection-fig8.png)

I ricercatori di sicurezza di Microsoft sono costantemente in lookout hello per le minacce. Hanno accesso tooan ampi di set di dati di telemetria acquisita dalla presenza di globale di Microsoft nel cloud hello e locale. Questa raccolta vasto e diverse dei set di dati consente Microsoft toodiscover nuovo attacco modelli e tendenze nei propri prodotti consumer ed enterprise di on-premise, nonché i servizi online.

Di conseguenza, il Centro sicurezza può aggiornare rapidamente gli algoritmi di rilevamento a fronte del rilascio di exploit nuovi e sofisticati da parte di utenti malintenzionati. Questo approccio consente di tenere il passo con un ambiente caratterizzato da minacce in rapida evoluzione.

![Centro sicurezza](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Rilevamento minacce del Centro sicurezza PC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso.  Viene avviata l'analisi di queste informazioni, la correlazione di informazioni da più origini, tooidentify minacce.
Avvisi di sicurezza sono classificati in Centro sicurezza PC insieme ai consigli su come tooremediate hello minaccia.

Il Centro sicurezza si avvale di analisi della sicurezza avanzate, che vanno ben oltre gli approcci basati sulle firme. Successi nei dati di grandi dimensioni e [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologie sono utilizzati tooevaluate eventi attraverso l'infrastruttura di cloud intera hello: rilevamento minacce che sarebbero Impossibile tooidentify approcci manuali e utilizzato per stimare hello evoluzione di attacchi. Questi analitica di sicurezza include seguente hello.

### <a name="threat-intelligence"></a>Intelligence per le minacce

Microsoft vanta un'enorme quantità di dati di intelligence per le minacce globali.
Flussi di dati di telemetria da più origini, ad esempio Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes Unit (DCU) e Microsoft Security Response Center (MSRC).

![Intelligence per le minacce](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

I ricercatori inoltre ricevano informazioni relative a minacce intelligence che viene condiviso tra i provider di servizi cloud principali e sottoscrive toothreat intelligence feed da terze parti. Centro sicurezza di Azure è possibile utilizzare questo tooalert informazioni si toothreats da noti cattivi attori. Di seguito sono riportati alcuni esempi:

-   **Sfruttando hello Power di Machine Learning -** Centro sicurezza di Azure dispone di accesso tooa grande quantità di dati sulle attività di rete cloud, che può essere utilizzato toodetect minacce per le distribuzioni di Azure. ad esempio:

-   **Rilevamenti di forza bruti -** Machine learning è toocreate utilizzato un modello cronologico di tentativi di accesso remoto, che consente la toodetect attacchi di forza bruta contro le porte SQL, RDP e SSH.

-   **In uscita DDoS e rilevamento Botnet** -un obiettivo comune di attacchi di risorse cloud di destinazione è toouse di potenza di calcolo di tooexecute queste risorse hello altri attacchi.

-   **Nuovo comportamento Analitica server e le macchine virtuali -** dopo che una macchina virtuale o il server è compromesso, aggressori un'ampia gamma di codice dannoso di tecniche tooexecute in tale sistema evitando di rilevamento, assicurandosi di persistenza e non dovranno controlli di sicurezza.

-   **Rilevamento minacce del Database SQL Azure -** rilevamento minacce per il Database di SQL Azure, che identifica l'attività del database anomale che indica di non comuni e potenzialmente dannoso tenta tooaccess o exploit database.

### <a name="behavioral-analytics"></a>Analisi del comportamento

Comportamento analitica è una tecnica che consente di analizzare e confrontare tooa raccolta dei dati di schemi noti. Tuttavia, questi modelli non sono semplici firme. Sono determinati tramite gli algoritmi di apprendimento machine complessi sono applicati toomassive set di dati.

![Analisi del comportamento](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Sono anche definiti tramite l'attento esame di comportamenti dannosi da parte di analisti esperti. Centro sicurezza di Azure è possibile utilizzare le risorse tooidentify compromesso analitica comportamentali in base all'analisi dei log di macchina virtuale, i registri di dispositivi di rete virtuale, i log dell'infrastruttura, dump di arresto anomalo e altre origini.

Inoltre, è la correlazione con altri toocheck segnali per il supporto di prova di una campagna generalizzata. Questa correlazione consente eventi tooidentify coerenti con stabiliti indicatori di compromissione.

Di seguito sono riportati alcuni esempi:
-   **Esecuzione del processo sospette:** aggressori diversi software dannoso in tooexecute tecniche senza il rilevamento. Ad esempio, un utente malintenzionato potrebbe fornire malware hello stessi nomi dei file di sistema legittimo ma posizionare i file in una posizione alternativa, utilizzare un nome che è molto simile a un file non grave, o maschera hello true estensione di file. Monitoraggi e i comportamenti di processi di Centro sicurezza PC modelli elaborare outlier toodetect esecuzioni come i seguenti.

-   **Tentativi di malware e sfruttamento delle vulnerabilità nascosto:** sofisticato malware può eludere prodotti antimalware tradizionale mai toodisk scrittura o la crittografia dei componenti software archiviati su disco. Tuttavia, il malware può essere rilevato tramite l'analisi della memoria, come malware hello necessario lasciare tracce in memoria toofunction. Quando si blocca software, un dump di arresto anomalo del sistema acquisisce una parte della memoria in fase di arresto anomalo di hello di hello. Analizzando memoria hello nel dump di arresto anomalo di hello, Centro sicurezza di Azure può rilevare le tecniche utilizzate tooexploit vulnerabilità nel software, accedere a dati riservati e furtivamente rende persistenti all'interno di un computer compromesso senza influenzare le prestazioni di hello di computer in uso.

-   **Laterali lo spostamento e l'esplorazione interno:** toopersist in un compromesso di rete e individuare/raccolto importante dei dati, spesso i pirati toomove lateralmente da hello compromesso tooothers computer all'interno di hello stessa rete. Centro sicurezza PC esegue il monitoraggio di processo e toodiscover le attività di accesso prova tooexpand di mercato rete hello, ad esempio l'esecuzione del comando remoto, rete sondaggio e di enumerazione di account all'interno di un utente malintenzionato.

-   **Script di PowerShell dannosi:** PowerShell è utilizzabile da codice dannoso di utenti malintenzionati tooexecute nelle macchine virtuali di destinazione per un diversi scopi. Il Centro sicurezza ispeziona l'attività di PowerShell alla ricerca di prove di attività sospette.

-   **In uscita attacchi:** gli utenti malintenzionati spesso le risorse di cloud con scopo hello dell'utilizzo di tali attacchi aggiuntive toomount di risorse di destinazione. Compromesse macchine virtuali, ad esempio, potrebbe essere dagli attacchi di forza bruta toolaunch utilizzate altre macchine virtuali, inviare posta indesiderata o analisi aprire le porte e altri dispositivi hello Internet. Tramite l'applicazione di machine learning toonetwork traffico, il Centro sicurezza PC in grado di rilevare quando le comunicazioni di rete in uscita superano la norma hello. Quando inviare posta indesiderata, Centro sicurezza PC correla anche il traffico di posta elettronica insolito con Business intelligence da Office 365 toodetermine se posta elettronica hello è probabile che nefandi o hello risultato di una campagna di posta elettronica legittimi.

### <a name="anomaly-detection"></a>Anomaly Detection

Centro sicurezza di Azure Usa anche minacce tooidentify rilevamento di anomalie. In analitica di toobehavioral contrasto (che dipende noti modelli che derivano dal set di dati di grandi dimensioni), il rilevamento di anomalie più "personalizzato" e si concentra su linee di base sono distribuzioni tooyour specifico. Machine learning è applicato toodetermine normale attività per le distribuzioni e quindi le regole sono le condizioni di outlier toodefine generato che potrebbe rappresentare un evento di protezione. Ecco un esempio:

-   **Attacchi di forza bruta RDP/SSH in ingresso**: nelle distribuzioni dei clienti possono essere presenti macchine virtuali occupate da molti accessi ogni giorno e altre con pochi o nessun accesso. Centro sicurezza di Azure è possibile determinare l'attività di accesso di base per le macchine virtuali e utilizzare machine learning toodefine intorno attività normale accesso hello. Se è presente una discrepanza con definita per la previsione hello correlate all'accesso alle caratteristiche, quindi può essere generato un avviso. Anche in questo caso, le tecniche di apprendimento automatico determinano gli eventi significativi.

### <a name="continuous-threat-intelligence-monitoring"></a>Monitoraggio continuo dell'intelligence per le minacce

Centro sicurezza di Azure funziona con protezione dati dell'analisi scientifica dei team di ricerca e in tutto il mondo hello che monitoraggio continuo per le modifiche minacce hello. Ad esempio hello iniziative di seguito:

-   **Monitoraggio dell'intelligence per le minacce**: questo tipo di intelligence include meccanismi, indicatori, implicazioni e consigli utili sulle minacce esistenti o emergenti. Queste informazioni sono condiviso nella community di sicurezza hello e Microsoft monitora costantemente threat intelligence feed da origini interne ed esterne.

-   **Condivisione dei segnali**: le informazioni dettagliate dai team della sicurezza nell'ampio portfolio di servizi, server e dispositivi endpoint client locali e cloud di Microsoft vengono condivise e analizzate.

-   **Specialisti della sicurezza Microsoft**: in contatto costante con i team Microsoft che operano in ambiti di sicurezza specializzati, ad esempio analisi scientifiche e rilevamento di attacchi Web.

-   **Ottimizzazione di rilevamento:** algoritmi vengono eseguiti sul set di dati reali di clienti e ricercatori di sicurezza utilizzano clienti toovalidate hello risultati. Veri e falsi positivi sono algoritmi utilizzati toorefine machine learning.

Queste attività combinata concludere rilevamenti nuovi e migliorati, è possibile trarre vantaggio da immediatamente: nessuna azione per si tootake.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Funzionalità di rilevamento delle minacce avanzato: altri servizi di Azure

### <a name="virtual-machine-microsoft-antimalware"></a>Macchina virtuale: Microsoft Antimalware

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) per Azure è una soluzione single-agent per le applicazioni e gli ambienti di tenant, progettato toorun in background hello senza intervento umano. È possibile distribuire la protezione in base alle esigenze di hello i carichi di lavoro dell'applicazione, con una base sicura-per impostazione predefinita o configurazione personalizzata, ad esempio il monitoraggio antimalware avanzata. Antimalware Azure è un'opzione di sicurezza per macchine virtuali di Azure e viene installato automaticamente in tutte le macchine virtuali PaaS di Azure.

**Funzionalità di Azure toodeploy e abilitare Microsoft Antimalware per le applicazioni**

#### <a name="microsoft-antimalware-core-features"></a>Funzionalità principali di Microsoft Antimalware

-   **Protezione in tempo reale -** monitora attività nei servizi Cloud e macchine virtuali toodetect e blocco di esecuzione di malware.

-   **Pianificate analisi -** esegue periodicamente destinazione analisi malware toodetect, inclusi i programmi in esecuzione.

-   **Correzione del malware**: interviene automaticamente sul malware rilevato, ad esempio eliminando o mettendo in quarantena i file dannosi e pulendo le voci dannose del Registro di sistema.

-   **Aggiornamenti firma -** automaticamente installa hello più recente protezione firme (definizioni di virus) tooensure dati sia aggiornato sulla frequenza predeterminata.

-   **Gli aggiornamenti del motore antimalware -** automaticamente gli aggiornamenti hello motore Antimalware Microsoft.

-   **Gli aggiornamenti della piattaforma antimalware –** automaticamente gli aggiornamenti hello piattaforma Microsoft Antimalware.

-   **Attiva la protezione dati -** indica i metadati di dati di telemetria sulle minacce e le risorse sospette tooMicrosoft tooensure Azure rapidi tempi di risposta toohello evoluzione panorama delle minacce e l'abilitazione di recapito firma sincrono in tempo reale tramite Hello Microsoft Active Protection System (MAPS).

-   **Esempi di creazione report -** fornisce e segnala gli esempi toohello Microsoft Antimalware service toohelp perfezionare servizio hello e abilitare la risoluzione dei problemi.

-   **Esclusioni:** consente l'applicazione e servizio amministratori tooconfigure determinati file, i processi e unità tooexclude di protezione e l'analisi delle prestazioni e/o altri motivi.

-   **Raccolta di eventi antimalware -** registra l'integrità del servizio antimalware hello, le attività sospette e azioni di correzione nel registro eventi di sistema operativo hello e li raccoglie in account di archiviazione di Azure del cliente hello.

### <a name="azure-sql-database-threat-detection"></a>Rilevamento delle minacce per il database SQL di Azure

[Rilevamento minacce del Database SQL Azure](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) è una nuova funzionalità di business intelligence di sicurezza incorporate hello servizio Database SQL di Azure. Risolvere hello clock toolearn, profilo e rilevare attività del database anomale, identifica di rilevamento minacce del Database SQL Azure database toohello di minacce potenziali.

I responsabili della sicurezza o altri amministratori designati possono ricevere una notifica immediata sulle attività di database sospette non appena si verificano. Ogni notifica fornisce i dettagli dell'attività sospette hello e suggerisce come toofurther analizzare e ridurre il rischio di hello.

Attualmente, il rilevamento delle minacce per il database SQL di Azure rileva vulnerabilità potenziali, attacchi SQL injection e modelli anomali di accesso ai database.

Alla ricezione di notifica tramite posta elettronica di rilevamento minacce, gli utenti sono in grado di toonavigate e visualizzazione hello controllo rilevanti record con collegamento diretto hello messaggio hello che apre un controllo visualizzatore e/o il preconfigurati controllo modello di Excel che Mostra controllo rilevanti hello record intorno hello ora di hello sospette evento in base toohello seguenti:
-   Archiviazione di controllo per hello/server di database con l'attività del database anomale hello

-   Tabella di archiviazione di controllo pertinente che è stata utilizzata in fase di hello del log di controllo di hello evento toowrite

-   Record di hello segue ora poiché hello evento si verifica di controllo.

-   Record di controllo con ID di evento simili in fase di hello dell'evento hello (facoltativo per alcuni rilevatori)

SQL Database minaccia rilevatori utilizzare uno dei hello seguendo le metodologie di rilevamento:

-   **Rilevamento deterministico –** rilevare modelli sospetti (basato su regole) in query del client SQL di hello corrispondenti attacchi noti. Questa metodologia è rilevamento alto e bassa falso positivo, è tuttavia limitata coverage perché rientra in una categoria di hello di "rilevamenti atomici".

-   **Rilevamento comportamento:** difetti anomalie dell'attività, ovvero un comportamento anomalo per i database hello che non è stato individuato durante hello ultimi 30 giorni.  Un esempio di attività anomale del client SQL può essere un picco di accessi non riuscite/query, volumi elevati di dati vengono estratti, insolita query canonica e familiarità IP indirizzi utilizzati tooaccess hello database

### <a name="application-gateway-web-application-firewall"></a>Web application firewall del gateway applicazione

[Web Application Firewall](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) è una funzionalità di [Gateway applicazione Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) tooweb applicazioni che usano gateway applicazione standard che fornisce la protezione [controllo recapito dell'applicazione](https://kemptechnologies.com/in/application-delivery-controllers) funzioni. Firewall applicazione Web esegue questa operazione di protezione contro la maggior parte delle hello [OWASP le prime 10 vulnerabilità web comuni](https://www.owasp.org/index.php/Top_10_2010-Main)

![Web application firewall del gateway applicazione](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Protezione dagli attacchi SQL injection

-   Protezione dagli attacchi di scripting intersito

-   Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion

-   Protezione dalle violazioni del protocollo HTTP

-   Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header

-   Prevenzione contro robot, crawler e scanner

-   Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)

Configurazione WAF al Gateway applicazione fornisce hello tooyou vantaggio seguenti:

-   Proteggere l'applicazione web da attacchi senza codice toobackend modifica e vulnerabilità di web.

-   Web più proteggere le applicazioni di hello stesso tempo dietro un gateway applicazione. Gateway applicazione supporta l'hosting di siti Web too20 dietro un singolo gateway che possono essere protette da attacchi di web.

-   Monitoraggio dell'applicazione Web contro gli attacchi tramite report in tempo reale generati dai log del WAF del gateway applicazione.

-   Alcuni controlli di conformità richiedono tutti i punti finali toobe protetto da una soluzione WAF è connessa a internet. Grazie al gateway applicazione con WAF abilitato è possibile soddisfare questi requisiti di conformità.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>API di rilevamento delle anomalie integrata in Azure Machine Learning

L'API di rilevamento delle anomalie è integrata in Azure Machine Learning e permette di rilevare i diversi tipi di modelli anomali nei dati delle serie temporali. Hello API assegna un'anomalia punteggio tooeach dati punto nella serie temporale hello, che può essere utilizzato per la generazione di avvisi, monitoraggio tramite Dashboard o la connessione con i sistemi di emissione di ticket.

Hello [API di rilevamento di anomalie](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) consente di rilevare i seguenti tipi di anomalie in dati della serie temporale hello:

-   **Picchi e DIP:** , ad esempio, durante il monitoraggio hello numero di account di accesso errori tooa servizio o un numero di estrazioni eseguite in un sito di e-commerce, picchi anomali o DIP potrebbe indicare gli attacchi alla sicurezza o interruzioni del servizio.

-   **Tendenze positive e negative:** durante il monitoraggio dell'utilizzo della memoria per l'elaborazione, ad esempio, una riduzione delle dimensioni della memoria disponibile può indicare una possibile perdita di memoria. Durante il monitoraggio della lunghezza della coda del servizio, una tendenza persistente verso l'alto può indicare un problema software sottostante.

-   **Livello di modifiche e le modifiche in un intervallo dinamico di valori:** , ad esempio, di modifica di livello delle latenze di un servizio dopo l'aggiornamento di un servizio o ridurre i livelli di eccezioni dopo l'aggiornamento può essere interessante toomonitor.

apprendimento Hello basato su API che supporta:

-   **Rilevamento flessibile e robusta:** modelli di rilevamento di anomalie hello consentono agli utenti di impostazioni di sensibilità tooconfigure e rilevare le anomalie tra set di dati stagionali e non stagionali. Gli utenti possano regolare hello rilevamento modello toomake hello il rilevamento di anomalie API meno o per esigenze più sensibili tootheir secondo. Ciò significa rilevamento hello maggiore o minore visibile eventuali anomalie nei dati con e senza modelli stagionali.

-   **Rilevamento scalabile e tempestivo:** utilizzo tradizionale di hello di monitoraggio con soglie presente l'impostazione di conoscenza degli esperti sono costosi e non scalabile toomillions di modificare dinamicamente i set di dati. i modelli di rilevamento di anomalie Hello in questa API vengono acquisiti e i modelli vengono ottimizzati automaticamente dai dati in tempo reale e cronologici.

-   **Rilevamento proattivo ed eseguibile:** è possibile applicare il rilevamento di tendenze lente e cambi di livello per rilevare in anticipo le anomalie. segnali anomala di Hello anticipata rilevati possono essere utilizzato toodirect comprensibile tooinvestigate e agire su aree problematiche hello.  Inoltre, è possibile sviluppare modelli di analisi della causa radice e gli strumenti di avviso sull'API di rilevamento delle anomalie.

rilevamento di anomalie Hello API è una soluzione efficace ed efficiente per un'ampia gamma di scenari come l'integrità del servizio e indicatori KPI di monitoraggio, IoT, il monitoraggio delle prestazioni e monitoraggio del traffico di rete. Di seguito sono riportati alcuni scenari comuni in cui questa API può risultare utile:
- I reparti IT necessario eventi tootrack strumenti, codice di errore, log di utilizzo e prestazioni (CPU, memoria e così via) in modo tempestivo.

-   Siti commerce online desiderano tootrack cliente attività, visualizzazioni di pagina, fa clic su e così via.

-   Utilità società si tootrack consumo di acqua, gas, energia elettrica e altre risorse.

-   Funzione/creazione di servizi di gestione desidera toomonitor temperatura, umidità, traffico e così via.

-   IoT/produttori desidera toouse sensore dati toomonitor serie tempo il flusso di lavoro, qualità e così via.

-   Provider di servizi, ad esempio call center tendenza di richiesta di servizio toomonitor, volume di eventi imprevisti, è necessario attendere lunghezza della coda e così via.

-   Gruppi di attività analitica desidera toomonitor business degli indicatori KPI (ad esempio, il volume delle vendite, i rispettivi clienti, prezzi) spostamento anomalo in tempo reale.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) è un componente fondamentale dello stack di Microsoft Cloud Security hello. È una soluzione completa che consente all'organizzazione quando si sposta tootake sfruttare appieno il potenziale hello delle applicazioni cloud, ma può rimanere in controllo mediante una migliore visibilità nelle attività. Consente inoltre di aumentare la protezione dei dati critici di hello tutte le applicazioni cloud.

Con strumenti che consentono di rilevare shadow IT, valutare il rischio, imporre criteri, esaminare le attività e arrestare le minacce, l'organizzazione in modo più sicuro possibile spostare toohello cloud mantenendo il controllo dei dati critici.

<table style="width:100%">
 <tr>
   <td>Scoprire</td>
   <td>Scoprire shadow IT con Cloud App Security. Ottenere visibilità tramite l'identificazione di app, attività, utenti, dati e file nell'ambiente cloud. Rilevare le app di terze parti connesse tooyour cloud.</td>
 </tr>
 <tr>
   <td>Analisi dei problemi</td>
   <td>Esaminare le app cloud mediante gli strumenti di analisi forense cloud toodeep-approfondimento in App rischiose, specifici utenti e i file nella rete. Trovare i modelli nei dati hello raccolti dal cloud. Generare report toomonitor del cloud.</td>

 </tr>
 <tr>
   <td>Controllo</td>
   <td>Ridurre il rischio impostando criteri e avvisi tooachieve il massimo controllo sul traffico di rete cloud. Usare Cloud App Security toomigrate il toosafe gli utenti, alternative di app cloud approvate.</td>

 </tr>
 <tr>
   <td>Proteggere</td>
   <td>Usare Cloud App Security toosanction o impedire alle applicazioni, applicare la prevenzione della perdita di dati, le autorizzazioni di controllo e la condivisione e generare avvisi e report personalizzati.</td>

 </tr>
 <tr>
   <td>Controllo</td>
   <td>Ridurre il rischio impostando criteri e avvisi tooachieve il massimo controllo sul traffico di rete cloud. Usare Cloud App Security toomigrate il toosafe gli utenti, alternative di app cloud approvate.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security integra la visibilità con il cloud tramite:

-   Utilizzo di Cloud Discovery toomap e identificare l'ambiente cloud e hello App cloud, l'organizzazione utilizza.


-   Approvazione e divieto di app nel cloud.



-   Uso di connettori app facili da distribuire che si avvalgono di API del provider per ottenere visibilità e governance delle app a cui ci si connette.

-   Controllo continuo grazie all'impostazione e all'ottimizzazione costante di criteri.

Nella raccolta di dati da queste origini, Cloud App Security esegue un'analisi sofisticata sui dati hello. Viene immediatamente avvisa l'utente tooanomalous attività e fornisce la visibilità completa dell'ambiente cloud. È possibile configurare un criterio di Cloud App Security e usarlo tooprotect tutto nell'ambiente cloud.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Funzionalità ATD di terze parti tramite Azure Marketplace

### <a name="web-application-firewall"></a>Web application firewall

Web application firewall controlla il traffico Web in ingresso e blocca SQL injection, attacchi tramite script da altri siti, caricamenti di malware, DDoS di applicazioni e altri attacchi destinati alle applicazioni Web. Inoltre analizza le risposte hello dai server back-end web hello per la prevenzione della perdita di dati (DLP). motore di controllo di accesso integrato Hello Abilita criteri di controllo di accesso granulare toocreate amministratori per l'autenticazione, autorizzazione e Accounting (AAA), che fornisce l'autenticazione avanzata alle organizzazioni e un controllo utente.

**In evidenza:**
-   Rileva e blocca SQL injection, attacchi tramite script da altri siti, caricamenti di malware, DDoS di applicazioni e altri attacchi destinati alle applicazioni.

-   Offre autenticazione e controllo di accesso.

-   Analisi di dati sensibili toodetect di traffico in uscita e in grado di mascherare o bloccare le informazioni di hello dalla perdita.

-   Accelera la consegna di hello del contenuto dell'applicazione web, utilizzando funzionalità quali la memorizzazione nella cache, la compressione e altre ottimizzazioni di traffico.

Di seguito sono riportati alcuni esempi di Web application firewall disponibili in Azure Marketplace:

[Barracuda Web Application Firewall Brocade virtuale Web Application Firewall (Brocade vWAF), Imperva SecureSphere & hello ThreatSTOP IP Firewall.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Passaggi successivi

- [Funzionalità di rilevamento del Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Funzionalità avanzate di rilevamento del Centro sicurezza di Azure consente tooidentify minacce attive per le risorse di Microsoft Azure e fornisce informazioni dettagliate hello necessari toorespond rapidamente.

- [Rilevamento delle minacce per il database SQL di Azure](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Rilevamento minacce del Database SQL Azure consente di risolvere i problemi riguardanti il database di tootheir minacce potenziali.
