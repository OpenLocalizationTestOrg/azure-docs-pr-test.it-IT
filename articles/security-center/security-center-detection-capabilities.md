---
title: "funzionalità aaaDetection nel Centro protezione di Azure | Documenti Microsoft"
description: "Questo documento consente di toounderstand funzionamento delle funzionalità di rilevamento Centro sicurezza di Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Funzionalità di rilevamento del Centro sicurezza di Azure
Questo documento vengono illustrate funzionalità avanzate di rilevamento del Centro sicurezza di Azure che consentono di identificare le risorse di Microsoft Azure di destinazione di minacce attive e fornisce che con insights hello necessari toorespond rapidamente.

> [!NOTE]
> Rilevamenti avanzati sono disponibili in hello Standard livello del Centro sicurezza di Azure. È disponibile una versione di valutazione gratuita di 60 giorni. È possibile eseguire l'aggiornamento da hello selezione tariffario hello [criteri di sicurezza](security-center-policies.md). Visitare [pagina Centro sicurezza PC](https://azure.microsoft.com/pricing/details/security-center/) toolearn più sui prezzi. 
> 
> 

## <a name="responding-tootodays-threats"></a>Risponde a minacce di tootoday
Sono state apportate modifiche significative minacce hello su hello ultimi 20 anni. In hello precedente, le aziende in genere solo era tooworry sulla manipolazione di siti web da utenti malintenzionati di singoli utenti interessati principalmente vedere "Impossibile cosa fanno". Oggi gli utenti malintenzionati sono molto più sofisticati e organizzati. Hanno spesso obiettivi finanziari e strategici specifici, Hanno inoltre toothem di risorse disponibili altre, come si può essere finanziati dal stati nazione o criminali.

Questo approccio ha portato a livello di aspetto professionale di classificazioni utente malintenzionato hello senza precedenti tooan. Non sono più interessati al danneggiamento del Web. Sono ora interessati a rubare informazioni conti finanziari e dati privati, ognuno dei quali può utilizzare toogenerate flussi di cassa sul mercato aperto hello o tooleverage una particolare business, posizione politico o militare. Anche altre relativi a tali utenti malintenzionati con un obiettivo finanziario sono pirati informatici hello che violano le persone e reti toodo danni tooinfrastructure.

In risposta, distribuire spesso varie soluzioni di punto, incentrati sul difesa perimetrale enterprise hello o endpoint cercando le firme attacchi noti. Queste soluzioni tendono toogenerate un volume elevato di avvisi di fedeltà bassa, che richiedono un tootriage analista di sicurezza e provare a utilizzare. La maggior parte delle organizzazioni non dispongono di tempo hello e competenze richieste toorespond toothese avvisi: pertanto molti passare giornalismo.  Nel frattempo, gli utenti malintenzionati si sono evoluti toosubvert i relativi metodi molte difese basato sulla firma e [adattare ambienti toocloud](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Nuovi approcci sono necessari toomore rapidamente identificare le minacce e velocizzare il rilevamento e la risposta. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Modalità di rilevamento e risponde toothreats Centro sicurezza di Azure
I ricercatori di sicurezza di Microsoft sono costantemente in lookout hello per le minacce. Hanno accesso tooan ampi di set di dati di telemetria acquisita dalla presenza di globale di Microsoft nel cloud hello e locale. Questa raccolta vasto e diverse dei set di dati consente Microsoft toodiscover nuovo attacco modelli e tendenze nei propri prodotti consumer ed enterprise di on-premise, nonché i servizi online. Di conseguenza, il Centro sicurezza può aggiornare rapidamente gli algoritmi di rilevamento a fronte del rilascio di exploit nuovi e sofisticati da parte di utenti malintenzionati. Questo approccio consente di tenere il passo con un ambiente caratterizzato da minacce in rapida evoluzione. 

Rilevamento minacce del Centro sicurezza PC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso. Viene avviata l'analisi di queste informazioni, correlazione spesso informazioni provenienti da più origini, tooidentify minacce. Avvisi di sicurezza sono classificati in Centro sicurezza PC insieme ai consigli su come tooremediate hello minaccia.

![Raccolta dati e presentazione del Centro sicurezza](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Il Centro sicurezza si avvale di analisi della sicurezza avanzate, che vanno ben oltre gli approcci basati sulle firme. Successi nei dati di grandi dimensioni e [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologie vengono sfruttate tooevaluate eventi attraverso l'infrastruttura di cloud intera hello: rilevamento minacce che sarebbero Impossibile tooidentify approcci manuali e utilizzato per stimare hello evoluzione di attacchi. Queste analisi della sicurezza includono: 

* **Integrato sulle minacce**: ha un aspetto per noti cattivi attori sfruttando globale sulle minacce da prodotti e servizi, Microsoft hello Microsoft Digital Crimes Unit (DCU), hello Microsoft Security Response Center (MSRC) ed esterne i feed.
* **Comportamento analitica**: applica il comportamento di schemi noti toodiscover dannoso. 
* **Rilevamento di anomalie**: statistica toobuild una linea di base cronologico di profilatura viene utilizzato. Avvisa sulle deviazioni dalle linee di base stabilite conformi tooa potenziali attacchi.

### <a name="threat-intelligence"></a>Intelligence per le minacce
Microsoft vanta un'enorme quantità di dati di intelligence per le minacce globali. Dati di telemetria fluiscono in da più origini, ad esempio Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes Unit (DCU) e Microsoft Security Response Center (MSRC). I ricercatori inoltre ricevano informazioni relative a minacce intelligence che viene condiviso tra i provider di servizi cloud principali e sottoscrive toothreat intelligence feed da terze parti. Centro sicurezza di Azure è possibile utilizzare questo tooalert informazioni si toothreats da noti cattivi attori. Di seguito sono riportati alcuni esempi:

* **Indirizzo IP dannoso di comunicazioni in uscita tooa**: il traffico in uscita tooa noto botnet o darknet probabilmente indica che la risorsa sia stata compromessa e un utente malintenzionato tenta tooexecute comandi su tali dati di sistema o exfiltrate. Centro sicurezza di Azure Confronta database minaccia globale del tooMicrosoft il traffico di rete e genera avvisi se rileva l'indirizzo IP dannoso di comunicazione tooa.

## <a name="behavioral-analytics"></a>Analisi del comportamento
Comportamento analitica è una tecnica che consente di analizzare e confrontare tooa raccolta dei dati di schemi noti. Tuttavia, questi modelli non sono semplici firme. Sono determinati tramite gli algoritmi di apprendimento machine complessi sono applicati toomassive set di dati. Sono anche definiti tramite l'attento esame di comportamenti dannosi da parte di analisti esperti. Centro sicurezza di Azure è possibile utilizzare le risorse tooidentify compromesso analitica comportamentali in base all'analisi dei log di macchina virtuale, i registri di dispositivi di rete virtuale, i log dell'infrastruttura, i dump di arresto anomalo del sistema e altre origini. 

Inoltre, è la correlazione con altri toocheck segnali per il supporto di prova di una campagna generalizzata. Questa correlazione consente eventi tooidentify coerenti con stabiliti indicatori di compromissione. Di seguito sono riportati alcuni esempi:

* **Esecuzione del processo sospette**: aggressori diversi software dannoso in tooexecute tecniche senza il rilevamento. Ad esempio, un utente malintenzionato potrebbe fornire malware hello stessi nomi dei file di sistema legittimo ma posizionare i file in una posizione alternativa, utilizzare un nome che è molto simile tooa grave o maschera hello true estensione di file. Monitoraggi e i comportamenti di processi di Centro sicurezza PC modelli elaborare outlier toodetect esecuzioni come i seguenti.  
* **Tentativi di malware e sfruttamento delle vulnerabilità nascosto**: malware più sofisticati è prodotti antimalware tradizionale in grado di tooevade mai toodisk scrittura o la crittografia dei componenti software archiviati su disco.  Tuttavia, il malware può essere rilevato tramite l'analisi della memoria, come malware hello necessario lasciare tracce in memoria in ordine toofunction. Quando si blocca software, un dump di arresto anomalo del sistema acquisisce una parte della memoria in fase di arresto anomalo di hello di hello.  Analizzando memoria hello nel dump di arresto anomalo di hello, Centro sicurezza di Azure può rilevare le tecniche utilizzate tooexploit vulnerabilità nel software, accedere a dati riservati e furtivamente vengono mantenute all'interno un computer senza influenzare le prestazioni di hello di compromesso computer in uso.
* **Laterali lo spostamento e l'esplorazione interno**: toopersist in un compromesso di rete e individuare/raccolto importante dei dati, spesso i pirati toomove lateralmente da hello compromesso tooothers computer all'interno di hello stessa rete. Centro sicurezza PC esegue il monitoraggio di processo e le attività di accesso in ordine toodiscover tenta tooexpand di mercato all'interno di enumerazione di account e di rete hello, ad esempio rete verifica esecuzione comando remoto, un utente malintenzionato.
* **Script di PowerShell dannosi**: PowerShell è utilizzato da codice dannoso di utenti malintenzionati tooexecute nelle macchine virtuali di destinazione per vari scopi. Il Centro sicurezza ispeziona l'attività di PowerShell alla ricerca di prove di attività sospette. 
* **In uscita attacchi**: gli utenti malintenzionati spesso le risorse di cloud con scopo hello dell'utilizzo di tali attacchi aggiuntive toomount di risorse di destinazione. Compromesso le macchine virtuali, ad esempio, potrebbe essere dagli attacchi di forza bruta toolaunch utilizzate altre macchine virtuali, inviare posta indesiderata o analizzare le porte aperte e altri dispositivi sulle hello internet. Tramite l'applicazione di machine learning toonetwork traffico, il Centro sicurezza PC in grado di rilevare quando le comunicazioni di rete in uscita superano la norma hello. In caso di hello di posta indesiderata, Centro sicurezza PC anche mette in correlazione traffico insolito posta elettronica e intelligence da Office 365 toodetermine se è probabile che la posta elettronica hello nefandi o hello risultato di una campagna di posta elettronica legittimi.  

### <a name="anomaly-detection"></a>Rilevamento anomalie
Centro sicurezza di Azure Usa anche minacce tooidentify rilevamento di anomalie. In analitica di toobehavioral contrasto (che dipende noti modelli che derivano dal set di dati di grandi dimensioni), il rilevamento di anomalie più "personalizzato" e si concentra su linee di base sono distribuzioni tooyour specifico. Machine learning è applicato toodetermine normale attività per le distribuzioni e quindi le regole sono le condizioni di outlier toodefine generato che potrebbe rappresentare un evento di protezione. Ecco un esempio:

* **Attacchi di forza bruta RDP/SSH in ingresso**: nelle distribuzioni dei clienti possono essere presenti macchine virtuali occupate da molti accessi ogni giorno e altre con pochi o nessun accesso. Centro sicurezza di Azure è possibile determinare l'attività di accesso di base per le macchine virtuali e utilizzare machine learning toodefine all'esterno dell'attività di accesso normale. Se il numero di hello degli account di accesso o l'ora hello dell'account di accesso hello o hello posizione da cui hello vengono richiesti gli account di accesso o altre caratteristiche correlate all'accesso è molto diverso dalla linea di base hello, potrebbe generato un avviso. Anche in questo caso, le tecniche di apprendimento automatico determinano gli eventi significativi.

## <a name="continuous-threat-intelligence-monitoring"></a>Monitoraggio continuo dell'intelligence per le minacce
Centro sicurezza di Azure opera protezione dati analisi scientifica dei team di ricerca e che il monitoraggio continuo per le modifiche minacce hello. Ad esempio hello iniziative di seguito:

* **Monitoraggio dell'intelligence per le minacce**: questo tipo di intelligence include meccanismi, indicatori, implicazioni e consigli utili sulle minacce esistenti o emergenti. Queste informazioni sono condiviso nella community di sicurezza hello e Microsoft monitora costantemente threat intelligence feed da origini interne ed esterne.
* **Condivisione dei segnali**: le informazioni dettagliate dai team della sicurezza nell'ampio portfolio di servizi, server e dispositivi endpoint client locali e cloud di Microsoft vengono condivise e analizzate. 
* **Specialisti della sicurezza Microsoft**: in contatto costante con i team Microsoft che operano in ambiti di sicurezza specializzati, ad esempio analisi scientifiche e rilevamento di attacchi Web.
* **Ottimizzazione di rilevamento**: algoritmi vengono eseguiti sul set di dati reali di clienti e ricercatori di sicurezza utilizzano clienti toovalidate hello risultati. Veri e falsi positivi sono algoritmi utilizzati toorefine machine learning.

Queste attività combinata concludere rilevamenti nuovi e migliorati, è possibile trarre vantaggio da immediatamente: nessuna azione per si tootake.

## <a name="see-also"></a>Vedere anche
In questo documento, è stato illustrato il funzionamento delle funzionalità di rilevamento tooAzure Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md)
* [La gestione e risponde avvisi toosecurity nel Centro protezione di Azure](security-center-managing-and-responding-alerts.md)
* [Avvisi di sicurezza per tipo nel Centro sicurezza di Azure](security-center-alerts-type.md)
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

