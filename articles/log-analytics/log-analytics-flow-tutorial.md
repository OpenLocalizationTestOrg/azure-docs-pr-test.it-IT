---
title: i processi di Azure Log Analitica aaaAutomate con Microsoft Flow
description: Informazioni su come utilizzare Microsoft Flow tooquickly automatizzare i processi ripetibili utilizzando il connettore di Azure Log Analitica hello.
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Automatizzare i processi di Log Analitica con connettore hello per Microsoft Flow
[Microsoft Flow](https://ms.flow.microsoft.com) consente con centinaia di azioni per un'ampia gamma di servizi flussi di lavoro toocreate automatizzata. Output da un'azione può essere usato come input tooanother consentendo toocreate integrazione tra diversi servizi.  connettore di Hello Analitica di Log di Azure per Microsoft Flow consentono toobuild flussi di lavoro che includono i dati recuperati dalle ricerche log nel Log Analitica.

Ad esempio, si può utilizzare dati di Log Analitica toouse Microsoft Flow una notifica di posta elettronica da Office 365, creare un bug in Visual Studio Team Services o invia un messaggio di flessibilità.  È possibile attivare un flusso di lavoro da una semplice pianificazione o con un'azione in un servizio connesso, ad esempio quando viene ricevuto un messaggio di posta elettronica o un tweet.  


> [!NOTE]
> Hello Azure Log Analitica connector per Microsoft Flow richiede che l'area di lavoro toobe aggiornato toohello nuovo Log Analitica linguaggio di query. È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).  

esercitazione Hello in questo articolo viene illustrato come un flusso che invia automaticamente toocreate hello risultati di una ricerca di log Log Analitica tramite posta elettronica, solo un esempio di come è possibile utilizzare i Log Analitica in Microsoft Flow. 


## <a name="step-1-create-a-flow"></a>Passaggio 1: Creare un flusso
1. Accedi troppo[Microsoft Flow](http://flow.microsoft.com)e selezionare **flussi My**.
2. Fare clic su **+ Crea da zero**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Passaggio 2: Creare un trigger per il flusso
1. Fare clic su **Search hundreds of connectors and triggers** (Cerca centinaia di connettori e trigger).
2. Tipo **pianificazione** nella casella di ricerca hello.
3. Selezionare **Pianificazione** e quindi selezionare **Pianificazione - Ricorrenza**.
4. In hello **frequenza** selezionare **giorno** e hello **intervallo** immettere **1**.<br><br>![Finestra di dialogo del trigger di Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Passaggio 3: Aggiungere un'azione di Log Analytics
1. Fare clic su **+ Nuovo passaggio** e quindi su **Aggiungi un'azione**.
2. Cercare **Log Analytics**.
3. Fare clic su **Azure Log Analytics - Run query and visualize results** (Eseguire una query e visualizzare i risultati).<br><br>![Finestra di esecuzione query di Log Analytics](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Passaggio 4: Configurare l'azione di hello Log Analitica

1. Specificare i dettagli di hello dell'area di lavoro inclusi hello sottoscrizione ID, gruppo di risorse e il nome dell'area di lavoro.
2. Aggiungere i seguenti Log Analitica query toohello hello **Query** finestra.  Questa è una semplice query di esempio che può essere sostituita con una qualsiasi altra query che restituisce dati.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Selezionare **tabella HTML** per hello **tipo di grafico**.<br><br>![Azione di Log Analytics](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Passaggio 5: Configurare la posta elettronica di toosend flusso hello

1. Fare clic su **Nuovo passaggio** e quindi su **+ Aggiungi un'azione**.
2. Cercare **Office 365 Outlook**.
3. Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).<br><br>![Finestra di selezione di Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Specificare l'indirizzo di posta elettronica hello del destinatario in hello **a** finestra e un oggetto per la posta elettronica hello in **soggetto**.
5. Fare clic nella hello **corpo** casella.  Verrà aperta la finestra **Contenuto dinamico** con i valori delle azioni precedenti.  
6. Selezionare **Corpo**.  Si tratta di risultati hello della query hello hello azione Analitica di Log.
6. Fare clic su **Mostra opzioni avanzate**.
7. In hello **è HTML** , quindi selezionare **Sì**.<br><br>![Finestra di configurazione della posta elettronica di Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Passaggio 6: Salvare e testare il flusso
1. In hello **nome flusso** casella, aggiungere un nome per il flusso e quindi fare clic su **creare flusso**.<br><br>![Salva flusso](media/log-analytics-flow-tutorial/flow06.png)
2. flusso Hello è stato creato, verrà eseguito dopo un giorno, ovvero hello alla pianificazione specificata. 
3. flusso di hello tooimmediately test, fare clic su **Esegui** e quindi **eseguire flusso**.<br><br>![Esegui flusso](media/log-analytics-flow-tutorial/flow07.png)
3. Al termine del flusso di hello, controllare i messaggi hello del destinatario hello specificato.  Deve aver ricevuto un messaggio e-mail con un seguente toohello simile corpo:<br><br>![Esempio di messaggio di posta elettronica](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni su [Ricerche log di Log Analytics](log-analytics-log-search-new.md).
- Altre informazioni su [Microsoft Flow](https://ms.flow.microsoft.com).



