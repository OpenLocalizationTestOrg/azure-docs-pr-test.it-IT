---
title: aaaGet avviato con un'area di lavoro di Azure Log Analitica | Documenti Microsoft
description: "È possibile iniziare a usare un'area di lavoro di Log Analytics in pochi minuti."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Introduzione a un'area di lavoro di Log Analytics
È possibile iniziare a usare rapidamente Azure Log Analytics, che consente di valutare dati di intelligence operativa ottenuti dall'infrastruttura IT. Questo articolo consente di esaminare, analizzare e agire con facilità sui dati raccolti *gratuitamente*.

In questo articolo funge da un tooLog introduzione Analitica con un breve toowalk esercitazione si attraverso una distribuzione minima in Azure in modo che è possibile iniziare a utilizzare il servizio di hello. contenitore logico di Hello in cui sono memorizzati i dati di gestione in Azure viene chiamato un'area di lavoro. Dopo aver esaminato queste informazioni e di valutazione completata, è possibile rimuovere l'area di lavoro valutazione hello. Questo articolo è un'esercitazione, quindi non fornisce indicazioni sui requisiti aziendali, sulla pianificazione o sull'architettura.

>[!NOTE]
>Se si utilizza hello Cloud di Microsoft Azure per enti pubblici, utilizzare [il monitoraggio di Azure per enti pubblici + documentazione relativa alla gestione](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) invece.

Ecco un rapido controllo tooget di processo utilizzato hello avviato:

![Diagramma del processo](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1 Creare un account Azure e accedere

Se si dispone già di un account Azure, è necessario toocreate uno toouse Analitica di Log. È possibile creare un [account gratuito](https://azure.microsoft.com/free/) con validità di 30 giorni, che consente di accedere a qualsiasi servizio di Azure.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate un account gratuito e accedere a
1. Seguire le direzioni di hello in [creare l'account di Azure gratuita](https://azure.microsoft.com/free/).
2. Passare toohello [portale di Azure](https://portal.azure.com) ed eseguire l'accesso.

## <a name="2-create-a-workspace"></a>2 Creare un'area di lavoro

passaggio successivo Hello è toocreate un'area di lavoro.

1. Nel portale di Azure hello, ricerca elenco hello dei servizi in hello Marketplace per *Analitica Log*, quindi selezionare **Analitica Log**.  
    ![Portale di Azure](./media/log-analytics-get-started/log-analytics-portal.png)
2. Fare clic su **crea**, quindi selezionare le opzioni per hello seguenti elementi:
   * **Area di lavoro OMS**: immettere un nome per l'area di lavoro.
   * **Sottoscrizione** : se si dispone di più sottoscrizioni, scegliere quello desiderato tooassociate nuova area di lavoro hello hello.
   * **Gruppo di risorse**
   * **Posizione**
   * **Piano tariffario**  
       ![Creazione rapida](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Fare clic su **OK** toosee un elenco delle aree di lavoro.
4. Selezionare un'area di lavoro toosee i dettagli in hello portale di Azure.       
    ![Dettagli dell'area di lavoro](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>Ricerca nei log toonew dell'area di lavoro aggiornamento 3
È stato rilasciato un nuovo linguaggio di query Log Analitica e in ordine tootake i vantaggi, è necessario tooconvert l'area di lavoro.  Se l'area di lavoro è ospitato nell'area di hello è stato aggiornato, verrà visualizzato un banner di colore viola in alto hello dell'area di lavoro si invitano è tooconvert. aggiornamento di Hello è assolutamente volontaria e non influisce sull'esperienza di utilizzo di Log Analitica e le soluzioni che aggiungere.  

Per ulteriori informazioni toounderstand hello vantaggi, considerazioni e tooupgrade di processo, vedere [ricerca nei log di aggiornamento di Azure Log Analitica toonew](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4 Aggiungere soluzioni e offerte di soluzioni

Aggiungere quindi le soluzioni e le offerte di soluzioni. Le soluzioni di gestione sono una raccolta di regole logiche, di visualizzazione e di acquisizione dei dati che forniscono metriche relative a un'area problematica specifica. Un'offerta di soluzioni è un raggruppamento di soluzioni di gestione.

Aggiunta dell'area di lavoro di soluzioni tooyour consente toocollect Log Analitica vari tipi di dati dai computer di area di lavoro tooyour connesso tramite agenti. Gli agenti di onboarding vengono illustrati più avanti.

### <a name="tooadd-solutions-and-solution-offerings"></a>soluzioni tooadd e le soluzioni offerte

1. Nel portale di Azure, fare clic su **New** e quindi in hello **marketplace hello ricerca** digitare **Analitica Log attività** e quindi premere INVIO.
2. Hello tutti gli elementi nel pannello seleziona **Analitica Log attività** e quindi fare clic su **crea**.  
    ![Activity Log Analytics](./media/log-analytics-get-started/activity-log-analytics.png)  
3. In hello *Nome soluzione di gestione* pannello, selezionare un'area di lavoro che si desidera tooassociate con la soluzione di gestione hello.
4. Fare clic su **Crea**.  
    ![area di lavoro della soluzione](./media/log-analytics-get-started/solution-workspace.png)  
5. Ripetere i passaggi da 1 a 4 tooadd:
    - Hello **sicurezza e conformità** con le soluzioni Antimalware Assessment e Security and Audit hello dell'offerta di servizio.
    - Hello **di automazione e controllo** offerta di servizio con hello lavoro ibridi di automazione, il rilevamento delle modifiche e soluzioni System Update Assessment (detto anche la gestione degli aggiornamenti). Quando si aggiunge l'offerta di soluzione hello, è necessario creare un account di automazione.  
        ![Account di Automazione](./media/log-analytics-get-started/automation-account.png)  
6. È possibile visualizzare le soluzioni di gestione hello aggiunto tooyour dell'area di lavoro passando troppo**Log Analitica** > **sottoscrizioni** > ***nome area di lavoro***  >  **Panoramica**. Vengono visualizzati i riquadri per soluzioni di gestione di hello che è stato aggiunto.  
    >[!NOTE]
    >Poiché un'area di lavoro toohello gli agenti non è stato ancora connesso, eventuali dati per le soluzioni hello aggiunto non vengono visualizzati.  

    ![riquadri delle soluzioni senza dati](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4 Creare una macchina virtuale ed eseguire l'onboarding di un agente

Creare quindi una semplice macchina virtuale in Azure. Dopo aver creato una macchina virtuale, hello onboard OMS agent tooenable è. Abilitazione dell'agente di hello inizia la raccolta dei dati da hello VM e invia dati tooLog Analitica.

### <a name="toocreate-a-virtual-machine"></a>toocreate una macchina virtuale

- Seguire le direzioni di hello in [creare la prima macchina virtuale di Windows nel portale di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md) e avviare hello nuova macchina virtuale.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Connessione macchina virtuale di hello tooLog Analitica

- Seguire le direzioni di hello in [tooLog di macchine virtuali di Azure connettersi Analitica](log-analytics-azure-vm-extension.md) tooconnect hello VM tooLog Analitica utilizzando hello portale di Azure.

## <a name="6-view-and-act-on-data"></a>6 Visualizzare i dati e definire le azioni necessarie

È abilitato in precedenza, soluzione Analitica Log attività hello e offerte di servizi di sicurezza, conformità e automazione & controllo hello. Verranno quindi esaminati i dati raccolti dalle soluzioni e i risultati delle ricerche nei log.

toostart, esaminare i dati visualizzati all'interno di soluzioni. Analizzare quindi le ricerche nei log a cui si accede dalla pagina corrispondente. Ricerche nei log consentono toocombine e correlare i dati dei computer da più origini all'interno dell'ambiente. Per ulteriori informazioni, vedere [Accedi ricerche Log Analitica](log-analytics-log-searches.md) o se è stato convertito l'area di lavoro toohello nuovo linguaggio di query, vedere [log comprensione di eseguire ricerche nei Log Analitica](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview dati Antimalware

1. Nel portale di Azure hello, passare troppo**Log Analitica** > ***l'area di lavoro***.
2. Nel pannello hello dell'area di lavoro, in **generale**, fare clic su **Panoramica**.  
    ![Panoramica](./media/log-analytics-get-started/overview.png)
3. Fare clic su hello **Antimalware Assessment** riquadro. Come si può notare in questo esempio, Windows Defender è installato in un computer, ma la firma non è aggiornata.  
    ![Antimalware](./media/log-analytics-get-started/solution-antimalware.png)
4. Per questo esempio, in **lo stato di protezione**, fare clic su **firma non aggiornata** tooopen ricerca nei Log e visualizzarne i dettagli sui computer hello che hanno firme aggiornate. In questo esempio, si noti che computer hello è denominato *getstarted*. Se ci sono più di un computer con firme aggiornate, tutti visualizzati in Log Search hello risultati.  
    ![Antimalware non aggiornato](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview dati Security and Audit

1. Nel pannello hello dell'area di lavoro, in **generale**, fare clic su **Panoramica**.  
2. Fare clic su hello **Security and Audit** riquadro. Come si può notare in questo esempio, esistono due problemi rilevanti: un computer privo di aggiornamenti critici e un computer con protezione insufficiente.  
    ![Sicurezza e controllo](./media/log-analytics-get-started/security-audit.png)
3. Per questo esempio, in **problemi rilevanti**, fare clic su **computer con aggiornamenti critici mancanti** tooopen ricerca nei Log e visualizzarne i dettagli sui computer con aggiornamenti critici mancanti. In questo esempio non sono presenti un aggiornamento critico e 63 aggiornamenti di altro tipo.  
    ![Sicurezza e controllo - Ricerca log](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview e agire sui dati di aggiornamento del sistema

1. Nel pannello hello dell'area di lavoro, in **generale**, fare clic su **Panoramica**.  
2. Fare clic su hello **System Update Assessment** riquadro. Come si può notare in questo esempio, è presente un computer Windows computer denominato *getstarted* che necessita di aggiornamenti critici, oltre a un computer che necessita di aggiornamenti delle definizioni.  
    ![Aggiornamenti del sistema](./media/log-analytics-get-started/system-updates.png)
3. Per questo esempio, in **gli aggiornamenti mancanti**, fare clic su **gli aggiornamenti critici** tooopen ricerca nei Log e visualizzarne i dettagli sui computer con aggiornamenti critici mancanti. In questo esempio è assente un aggiornamento ed è presente un aggiornamento obbligatorio.  
    ![Aggiornamenti del sistema - Ricerca log](./media/log-analytics-get-started/system-updates-log-search.png)
4. Passare toohello [Operations Management Suite](http://microsoft.com/oms) sito Web e accedere con l'account di Azure. Dopo l'accesso, si noti che le informazioni della soluzione hello toowhat simile visualizzati nel portale di Azure hello.  
    ![Portale di OMS](./media/log-analytics-get-started/oms-portal.png)
5. Fare clic su hello **gestione aggiornamenti** riquadro.
6. Nel dashboard di gestione aggiornamento hello, si noti che le informazioni di aggiornamento del sistema hello toohello aggiornamenti del sistema informazioni simili che visti in hello portale di Azure. Tuttavia, hello **gestire le distribuzioni di aggiornamenti** riquadro è nuovo. Fare clic su hello **gestire le distribuzioni di aggiornamenti** riquadro.  
    ![Riquadro Gestione aggiornamenti](./media/log-analytics-get-started/update-management.png)
7. In hello **aggiornare le distribuzioni** pagina, fare clic su **Aggiungi** toocreate un *operazione di aggiornamento*.  
    ![Distribuzioni di aggiornamento](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  In hello **nuovo Update Deployment** pagina, digitare un nome per la distribuzione degli aggiornamenti hello, selezionare i computer tooupdate (in questo esempio, *getstarted*), scegliere una pianificazione e quindi fare clic su **salvare**.  
    ![Nuova distribuzione](./media/log-analytics-get-started/new-deployment.png)  
    Dopo aver salvato la distribuzione di aggiornamenti hello, vedrai hello pianificata aggiornare.  
    ![aggiornamento pianificato](./media/log-analytics-get-started/scheduled-update.png)  
    Al termine dell'operazione di aggiornamento hello, hello Mostra stato **completato**.
    ![Aggiornamento completato](./media/log-analytics-get-started/completed-update.png)
9. Al termine dell'operazione di aggiornamento hello, è possibile visualizzare se hello esecuzione è riuscita o meno e sarà possibile visualizzare informazioni dettagliate su quali aggiornamenti all'applicazione.

## <a name="after-evaluation"></a>Dopo la valutazione

In questa esercitazione è stato installato un agente in una macchina virtuale e sono state eseguite rapidamente le operazioni iniziali. passaggi di Hello eseguiti sono state semplice e rapido. La maggior parte delle organizzazioni e delle aziende di grandi dimensioni, tuttavia, ha infrastrutture IT locali complesse. In tal caso, la raccolta dei dati da tali ambienti complessi richiede pianificazione e impegno aggiuntive rispetto a esercitazione hello. Esaminare le informazioni nella seguente sezione passaggi successivi per gli articoli toohelpful collegamenti hello hello.

È anche possibile rimuovere l'area di lavoro hello creato in questa esercitazione.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni sulla connessione [degli agenti Windows](log-analytics-windows-agents.md) tooLog Analitica.
* Informazioni sulla connessione [gli agenti di Operations Manager](log-analytics-om-agents.md) tooLog Analitica.
* [Aggiungere soluzioni Analitica Log da hello Solutions Gallery](log-analytics-add-solutions.md) tooadd funzionalità e raccolta dati.
* Acquisire familiarità con [log ricerche](log-analytics-log-searches.md) tooview dettagliate informazioni raccolte da soluzioni.
