---
title: gli eventi imprevisti toosecurity aaaRespond con Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento illustra come toouse centro di sicurezza di Azure per uno scenario di risposta agli eventi imprevisti.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Uso del Centro sicurezza di Azure per rispondere a un evento imprevisto
Molte organizzazioni informazioni su come gli eventi imprevisti toosecurity toorespond solo dopo aver subito un attacco. i costi tooreduce e danni, è importante toohave un intervento piano prima di un attacco ha luogo. Centro sicurezza di Azure può essere usato nelle diverse fasi della risposta agli eventi imprevisti.

## <a name="incident-response-planning"></a>Pianificazione della risposta agli eventi imprevisti
Un piano efficace dipende da tre funzionalità di base: essendo in grado di tooprotect, rilevare e rispondere toothreats. Protezione è su come evitare gli eventi imprevisti, rilevamento è sull'identificazione delle minacce all'inizio e risposta sta rimuovendo l'autore dell'attacco hello e il ripristino impatti hello toomitigate di sistemi di una violazione.

In questo articolo utilizzerà le fasi di risposta agli eventi imprevisti di protezione hello da hello [risposta di sicurezza di Microsoft Azure nel Cloud hello](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) articolo, come illustrato nel seguente diagramma hello:

![Ciclo di vita della risposta agli eventi imprevisti](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Durante le fasi di hello rileva problemi, valutare e diagnosticare, è possibile utilizzare il Centro sicurezza PC. Ecco alcuni esempi di come Centro sicurezza PC possono essere utili durante le fasi iniziali di risposta agli eventi imprevisti tre hello:

* **Rilevare**: esaminare prima indicazione di hello di un'indagine di eventi.
  * Esempio: revisione hello verifica iniziale che è stato generato un avviso di sicurezza con priorità alta nel dashboard di hello Centro sicurezza PC.
* **Valutare**: eseguire hello valutazione iniziale tooobtain ulteriori informazioni sulle attività sospette hello.
  * Esempio: ottenere ulteriori informazioni sull'avviso di sicurezza hello.
* **Diagnosi**: conduzione di un'analisi tecnica, identificazione di strategie di contenimento, mitigazione e di soluzioni alternative.
  * Esempio: seguire i passaggi correttivi hello descritti da Centro sicurezza PC nell'avviso di protezione.

scenario di Hello che segue viene illustrato come centro di sicurezza tooleverage durante hello rileva problemi, valutare e diagnosticare/rispondono fasi di un problema di sicurezza. Nel Centro sicurezza, un [evento imprevisto della sicurezza](security-center-incident.md) è un'aggregazione di tutti gli avvisi relativi a una risorsa, in linea con i modelli delle [catene di attacco](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/). Eventi imprevisti sono visualizzati in hello [degli avvisi di sicurezza](security-center-managing-and-responding-alerts.md) riquadro e blade. Un evento imprevisto, viene visualizzato per ulteriori informazioni su ogni occorrenza hello elenco avvisi correlati, che consente di tooobtain. Centro sicurezza PC presenta anche autonomo degli avvisi di sicurezza che possono essere anche usato tootrack verso il basso di un'attività sospetta.

## <a name="scenario"></a>Scenario
Contoso recentemente eseguita la migrazione alcune delle loro tooAzure risorse locali, inclusi alcuni carichi di lavoro line-of-business basati su macchine virtuali e database SQL. Il team di risposta agli eventi imprevisti della sicurezza di Contoso ha attualmente difficoltà nell'analisi dei problemi di sicurezza, data la mancanza di una intelligence di sicurezza integrata con gli attuali strumenti di risposta agli eventi imprevisti. La mancanza di integrazione introduce un problema durante la fase di rilevamento (troppi falsi positivi) hello, nonché durante la valutazione hello e diagnosticare fasi. Come parte di questa migrazione, ha deciso tooopt in Centro sicurezza PC toohelp loro indirizzo di questo problema.

Hello prima fase della migrazione completata dopo caricate tutte le risorse e tutti i consigli relativi alla sicurezza hello dall'area di sicurezza. CSIRT Contoso è il punto focale hello per la gestione dei problemi di sicurezza di computer. il team di Hello è costituito da un gruppo di persone con la responsabilità di affrontare eventuali problemi di sicurezza. chiaramente definiti dai membri del team Hello tooensure compiti rimasti senza un'area della risposta sono stati rilevati.

A scopo di hello di questo scenario, verrà toofocus nei ruoli hello di hello personalità che fanno parte di Contoso CSIRT seguenti:

![Ciclo di vita della risposta agli eventi imprevisti](./media/security-center-incident-response/security-center-incident-response-fig2.png)

Alice si occupa delle attività di sicurezza. Le sue responsabilità includono:

* Monitorare e rispondere minacce toosecurity intorno clock hello.
* Escalation di proprietario del carico di lavoro toohello cloud o un analista di sicurezza in base alle esigenze.

Guido è un analista della sicurezza e le sue responsabilità includono:

* Analisi degli attacchi.
* Risoluzione degli avvisi.
* Utilizzo di toodetermine proprietari del carico di lavoro e applica le misure di attenuazione.

Come si può notare, Alice e Sam hanno responsabilità diverse e devono interagire tra loro informazioni Centro sicurezza PC tooshare.

## <a name="recommended-solution"></a>Soluzione consigliata
Poiché Alice e Sam ruoli diversi, si useranno diverse aree di informazioni rilevanti tooobtain di centro di sicurezza per le attività quotidiane. Alice userà gli **avvisi di sicurezza** nell'ambito delle attività di monitoraggio giornaliere.

![Avvisi di sicurezza](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Alice userà gli avvisi di sicurezza durante hello rileva problemi e le fasi di valutazione. Al termine di valutazione iniziale hello, Alice lei potrebbe inoltrare hello problema tooSam se è necessaria un'ulteriore analisi. A questo punto, Sam utilizzerà informazioni hello fornito dal Centro sicurezza PC, talvolta in combinazione con altre origini dati, toomove toohello diagnosticare fase.

## <a name="how-tooimplement-this-solution"></a>Come tooimplement questa soluzione
toosee come si utilizzerebbe Centro sicurezza di Azure in uno scenario di risposta agli eventi imprevisti, verrà passaggi di Alice nelle fasi di rilevare e valutare hello e quindi vedere cosa Sam problema hello toodiagnose.

### <a name="detect-and-assess-incident-response-stages"></a>Fasi di rilevamento e valutazione nella risposta agli eventi imprevisti della sicurezza
Alice firmato toohello portale di Azure ed è funzionante nella console di hello Centro sicurezza PC. Come parte della propria giornaliera monitoraggio delle attività, ha avviato la revisione di sicurezza con priorità alta avvisi eseguendo hello alla procedura seguente:

1. Fare clic su hello **degli avvisi di sicurezza** hello riquadro e l'accesso **degli avvisi di sicurezza** blade.
    ![Pannello Avvisi di sicurezza](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > A scopo di hello di questo scenario, Alice è tooperform corso una valutazione su avviso di attività hello SQL dannosi, come illustrato nella figura precedente hello.
   >
   >
2. Fare clic su hello **attività SQL dannoso** avviso ed esaminare risorse hello attaccato hello **attività SQL dannoso** pannello: ![dettagli dell'evento imprevisto](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    In questo pannello, Alice può richiedere note relative risorse hello attaccato, come si sono verificati più volte questo tipo di attacco e quando è stata rilevata.
3. Fare clic su hello **attaccato risorsa** tooobtain ulteriori informazioni su questo tipo di attacco.

Dopo aver letto descrizione hello, Alice è convinti che non si tratta di un falso positivo e che lei deve inoltrare tooSam questo case.

### <a name="diagnose-incident-response-stage"></a>Fase di diagnosi nella risposta agli eventi imprevisti della sicurezza
SAM riceve case hello da Alice e inizia a esaminare i passaggi correttivi hello che suggeriti Centro sicurezza PC.

![Ciclo di vita della risposta agli eventi imprevisti](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Risorse aggiuntive
il team di risposta agli eventi imprevisti Hello può avvalersi di hello [sicurezza Center Power BI](security-center-powerbi.md) tipi diversi di toosee funzionalità di report. Questi report possono aiutarlo durante l'ulteriore analisi toovisualize, analizzare e filtrare indicazioni e degli avvisi di sicurezza. Per le aziende che utilizzano le relative informazioni di sicurezza e di una soluzione di gestione (SIEM) evento durante il processo di analisi hello, questi possono anche [integrare Centro sicurezza PC con la propria soluzione](security-center-integrating-alerts-with-log-integration.md). È inoltre possibile integrare i log di controllo di Azure e gli eventi di sicurezza di macchina virtuale (VM) utilizzando hello [strumento di integrazione di Azure log](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). tooinvestigate un attacco, è possibile utilizzare queste informazioni insieme a informazioni hello che fornisce il Centro sicurezza PC.

## <a name="conclusion"></a>Conclusioni
Mettere insieme un team, prima che si verifichi un evento imprevisto è molto importante tooyour organizzazione ne risentirà positivamente la modalità di gestione eventi imprevisti. Indisponibilità di risorse di hello strumenti giusti toomonitor consente questa tooremediate di passaggi accurate tootake team problemi di sicurezza. Centro sicurezza PC [funzionalità di rilevamento](security-center-detection-capabilities.md) può assistere eventi imprevisti di toosecurity IT tooquickly rispondere e correggere i problemi di sicurezza.
