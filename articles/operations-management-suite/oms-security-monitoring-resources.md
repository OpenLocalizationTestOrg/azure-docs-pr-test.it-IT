---
title: le risorse nella soluzione di controllo e protezione di Operations Management Suite aaaMonitoring | Documenti Microsoft
description: "Questo documento consente si toouse sicurezza OMS e toomonitor funzionalità di controllo delle risorse e identificare i problemi di sicurezza."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Monitoraggio delle risorse con la soluzione Security and Audit di Operations Management Suite
Questo documento consente di usare la sicurezza di OMS e toomonitor funzionalità di controllo delle risorse e identificare i problemi di sicurezza.

## <a name="what-is-oms"></a>Cos'è OMS?
Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Per ulteriori informazioni su OMS, leggere l'articolo hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Monitoraggio delle risorse
Ogni volta che è possibile, si desidererà eventi di sicurezza tooprevent accada in primo luogo hello. Tuttavia, è Impossibile tooprevent tutti gli eventi di sicurezza. Quando si verificano problemi di sicurezza, è necessario che l'impatto è ridotta a icona tooensure.  Esistono tre indicazioni importanti che possono essere utilizzati toominimize hello numero e hello impatto degli eventi imprevisti di protezione:

* Valutare periodicamente le vulnerabilità nel proprio ambiente.
* Controllare regolarmente tutti i sistemi di computer e tooensure di dispositivi di rete che hanno tutte hello patch più recenti installate.
* Controllare periodicamente tutti i log e i meccanismi di registrazione, inclusi i log eventi del sistema operativo, i log specifici dell'applicazione e i log di sistema di rilevamento delle intrusioni.

OMS Security and Audit consente di soluzioni IT tooactively monitorare tutte le risorse, che consentono di ridurre al minimo l'impatto di hello di eventi di sicurezza. Security and Audit di OMS dispone dei domini di sicurezza che possono essere utilizzati per il monitoraggio delle risorse. domini di sicurezza Hello consente di accedere rapidamente tooa opzioni, per hello monitoraggio di sicurezza seguenti domini verranno trattati in altri dettagli:

* Valutazione di software dannoso
* Valutazione degli aggiornamenti
* Identità e accesso

> [!NOTE]
> Per una panoramica di tutte queste opzioni, leggere [Introduzione alla soluzione Security and Audit di Operations Management Suite](oms-security-getting-started.md)
> 
> 

### <a name="monitoring-system-protection"></a>Protezione del sistema di monitoraggio
In una soluzione di protezione avanzata, è importante per hello ogni livello di protezione generale dello stato di sicurezza dell'asset. Computer con rilevato minacce e i computer con protezione insufficiente vengono visualizzati nella hello riquadro Malware Assessment in domini di sicurezza. Utilizzando le informazioni di hello in hello Malware Assessment, è possibile identificare una pianificazione tooapply protezione toohello dei server che ne hanno necessità. tooaccess hello di seguire questa opzione passaggi riportati di seguito.

1. In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **Security and Audit** riquadro.
   
    ![Security and Audit](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. In hello **Security and Audit** dashboard, fare clic su **Antimalware Assessment** in **domini di sicurezza**. Hello **Antimalware Assessment** dashboard viene visualizzato come illustrato di seguito:

![Valutazione di software dannoso](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

È possibile utilizzare hello **Malware Assessment** hello tooidentify dashboard problemi di sicurezza seguenti:

* **Minacce attive**: i computer sono stati compromessi e minacce attive nel sistema hello.
* **Risolti minacce**: i computer che sono stati compromessi ma minacce hello risolte.
* **Firma non aggiornata**: computer che dispongono di malware protection attivato ma firma hello è scaduta.
* **Nessuna protezione in tempo reale**: computer che non dispongono di un antimalware installato.

### <a name="monitoring-updates"></a>Monitoraggio degli aggiornamenti
L'applicazione di aggiornamenti della sicurezza più recenti hello è una protezione ottimale e deve essere incorporato nella strategia di gestione di aggiornamento. Il servizio Microsoft Monitoring Agent (HealthService.exe) legge informazioni sull'aggiornamento dai computer monitorati e invia quindi il servizio di informazioni aggiornate toohello OMS nel cloud hello per l'elaborazione. Hello servizio Microsoft Monitoring Agent è configurato come un servizio automatico e dovrebbe essere sempre in esecuzione nel computer di destinazione hello.

![Monitoraggio degli aggiornamenti](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Logica è applicato toohello aggiornare i dati e dati hello vengono registrati nel servizio cloud di hello. Se vengono rilevati aggiornamenti mancanti, vengono visualizzati nella hello **aggiornamenti** dashboard. È possibile utilizzare hello **aggiornamenti** toowork dashboard con mancante Aggiorna e sviluppare un piano tooapply li toohello server che ne hanno bisogno. Eseguire operazioni di hello seguenti hello tooaccess **aggiornamenti** dashboard:

1. In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **Security and Audit** riquadro.
2. In hello **Security and Audit** dashboard, fare clic su **Update Assessment** in **domini di sicurezza**. verrà visualizzato il dashboard di aggiornamento Hello come illustrato di seguito:

![Valutazione degli aggiornamenti](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

In questo dashboard è possibile eseguire un aggiornamento valutazione toounderstand hello stato corrente del computer e affrontare le minacce principali di hello. Utilizzando hello **critico o gli aggiornamenti della sicurezza** riquadro, gli amministratori IT sarà in grado di tooaccess informazioni dettagliate su aggiornamenti hello mancanti, come illustrato di seguito:

![Risultato della ricerca](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Questo report include informazioni critiche che possono essere utilizzato il tipo di hello tooidentify di minaccia per questo sistema è vulnerabile a, che include gli articoli della Microsoft KB hello associati con l'aggiornamento della sicurezza hello e hello Bulletin MS che include informazioni dettagliate sulle hello vulnerabilità.

### <a name="monitoring-identity-and-access"></a>Monitoraggio di identità e accesso
Con gli utenti che lavorano ovunque, utilizzano diversi dispositivi e l'accedono a una grande quantità di app sul cloud e in locale, è fondamentale che le credenziali siano protette. Attacchi con furto di credenziali sono quelle in cui un utente malintenzionato inizialmente Ottiene tooaccess le credenziali di accesso tooa regolari dell'utente un sistema all'interno di rete hello. In molti casi, questo attacco iniziale è solo una modo tooget toohello rete con accesso, obiettivo hello è l'account con privilegi toodiscover. 

Gli utenti malintenzionati verranno mantenuta nella rete hello, utilizzando gli strumenti credenziali tooextract dalle sessioni hello di altri account connesso disponibile gratuitamente. A seconda della configurazione del sistema hello, queste credenziali possono essere estratti in forma di hello di hash, il ticket o password non crittografate anche.  

> [!NOTE]
> computer che sono direttamente esposti toohello che verrà visualizzato Internet molti non è stato possibile tenta tale toologin try utilizzando tutti i tipi di nomi utente noti (ad esempio amministratore). Nella maggior parte dei casi è OK se non vengono utilizzati i nomi utente noti hello e password hello è sufficientemente complessa.
> 
> 

Si è tooidentify possibili intrusioni prima che essi compromettere un account con privilegi. È possibile sfruttare **soluzione di controllo e sicurezza OMS** toomonitor identità e accessi. Eseguire operazioni di hello seguenti hello tooaccess **identità e accessi** dashboard:

1. In hello **Microsoft Operations Management Suite** dashboard principale, fare clic su sicurezza e controllo riquadro.
2. In hello **Security and Audit** dashboard, fare clic su **identità e accessi** in **domini di sicurezza**. Hello **identità e accessi** dashboard viene visualizzato come illustrato di seguito:

![Identità e accesso](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Come parte della strategia di monitoraggio regolare, è necessario includere il monitoraggio dell’identità. L’amministratore IT dovrebbe verificare se è presente un nome utente valido specifico con un elevato numero di tentativi di accesso. Questo potrebbe indicare un utente malintenzionato che acquisito username reale hello e provare toobrute force o uno strumento automatico che Usa password hardcoded scaduti.

Questo Abilita dashboard tooquickly IT di identificare risorse del potenziali minacce correlate tooidentity e accesso toocompany. È determinato importante tooalso identificare le tendenze potenziali, ad esempio nel riquadro di hello accessi nel tempo, è possibile visualizzare periodo di tempo quante volte è stato eseguito un tentativo di accesso non riuscito. In questo caso hello computer **FileServer** ricevuto 35 tentativi di accesso. È possibile scoprire ulteriori dettagli su questo computer facendo clic su di esso. 

![Altre informazioni](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

report Hello generato per questo computer offre informazioni utili su questo modello. Notare che hello **ACCOUNT** consente di colonna hello gli account utente utilizzato tootry tooaccess hello sistema, hello **TIMEGENERATED** consente di colonna hello intervallo di tempo in cui hello tentativo è stato eseguito e Hello **LOGONTYPENAME** consente di colonna hello percorso in cui è stato eseguito questo tentativo. Se questi tentativi eseguiti localmente nel sistema hello da un programma, hello **processo** colonna sarebbe che mostra il nome del processo di hello. In scenari in cui il tentativo di accesso di hello proviene da un programma, si dispone già di nome di processo hello disponibile e ora è possibile eseguire un'ulteriore analisi nel sistema di destinazione hello.

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come toomonitor di soluzioni OMS Security and Audit toouse le risorse. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Introduzione alla soluzione Sicurezza e controllo di Operations Management Suite](oms-security-getting-started.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)

