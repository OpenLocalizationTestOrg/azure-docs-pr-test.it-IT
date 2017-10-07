---
title: i processi di Azure Application Insights aaaAutomate con Microsoft Flow
description: Informazioni su come utilizzare Microsoft Flow tooquickly automatizzare i processi ripetibili utilizzando il connettore di Application Insights hello.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Automatizzare i processi di Azure Application Insights con connettore hello per Microsoft Flow

È possibile trovare autonomamente ripetutamente in hello stesse query il toocheck di dati di telemetria che il servizio funziona correttamente? Tooautomate esaminando queste query per individuare tendenze e anomalie e quindi compilare i propri flussi di lavoro attorno a esse? il connettore di Azure Application Insights Hello (anteprima) per Microsoft Flow è strumento appropriato hello per questi scopi.

Con questa integrazione è ora possibile automatizzare numerosi processi senza dover scrivere codice. Dopo aver creato un flusso utilizzando un'azione di Application Insights, flusso hello esegue automaticamente la query di Application Insights Analitica. 

È possibile aggiungere anche altre azioni. In Microsoft Flow sono disponibili centinaia di azioni. Ad esempio, è possibile utilizzare Microsoft Flow tooautomatically invia una notifica tramite e-mail o creare un bug in Visual Studio Team Services. È inoltre possibile utilizzare uno dei hello molti [modelli](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) che sono disponibili per il connettore di hello per Microsoft Flow. Aumento della velocità questi modelli di processo hello di creazione di un flusso. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Creare un flusso per Application Insights

In questa esercitazione si apprenderà come toocreate attributi di un flusso che utilizza hello Analitica automatica cluster algoritmo toogroup nei dati di hello per un'applicazione web. flusso Hello invia automaticamente i risultati di hello tramite posta elettronica, solo un esempio di come è possibile utilizzare Microsoft Flow e Application Insights Analitica contemporaneamente. 

### <a name="step-1-create-a-flow"></a>Passaggio 1: Creare un flusso
1. Accedi troppo[Microsoft Flow](http://flow.microsoft.com), quindi selezionare **flussi My**.
2. Fare clic su **Crea un flusso da un modello vuoto**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Passaggio 2: Creare un trigger per il flusso
1. Selezionare **Pianificazione** e quindi selezionare **Pianificazione - Ricorrenza**.
2. In hello **frequenza** , quindi selezionare **giorno**e in hello **intervallo** immettere **1**.

    ![Finestra di dialogo del trigger di Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Passaggio 3: Aggiungere un'azione di Application Insights
1. Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.
2. Cercare **Azure Application Insights**.
3. Fare clic su **Application Insights - Visualize Analytics query Preview** (Application Insights - Visualizza query di Analisi Anteprima).

    ![Finestra di esecuzione della query di Analisi](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Passaggio 4: Connettere la risorsa di Application Insights tooan

toocomplete questo passaggio, è necessario un ID applicazione e una chiave API per la risorsa. È possibile recuperarli dal portale di Azure hello, come illustrato nel seguente diagramma hello:

![ID dell'applicazione nel portale di Azure hello](./media/app-insights-automate-with-flow/appid.png) 

- Specificare un nome per la connessione, insieme a hello applicazione ID e la chiave API.

    ![Finestra di connessione di Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Passaggio 5: Specificare hello query Analitica e tipo di grafico
Questo esempio di query Seleziona le richieste di hello non riuscito all'interno di hello ultimo giorno e li correla le eccezioni che si è verificato come parte dell'operazione di hello. Analitica li correla in base all'identificatore hello operation_Id. query Hello segmenti quindi risultati hello utilizzando l'algoritmo autocluster hello. 

Quando si crea la propria query, verificare che funzionino correttamente in Analitica prima di aggiungerlo tooyour flusso.

- Aggiungere hello seguente query Analitica e quindi selezionare tipo di grafico di tabella HTML hello. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Finestra di configurazione della query di Analisi](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Passaggio 6: Configurare la posta elettronica di toosend flusso hello

1. Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.
2. Cercare **Office 365 Outlook**.
3. Fare clic su **Office 365 Outlook - Invia un messaggio di posta elettronica**.

    ![Finestra di selezione di Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. In hello **invia un messaggio di posta elettronica** finestra hello seguenti:

   a. Digitare l'indirizzo di posta elettronica hello del destinatario hello.

   b. Digitare un oggetto per la posta elettronica hello.

   c. Fare clic nella hello **corpo** casella e quindi su hello contenuto menu dinamico che consente di aprire hello destro, selezionare **corpo**.

   d. Fare clic su **Mostra opzioni avanzate**.

    ![Configurazione di Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. Nel menu del contenuto dinamico hello hello seguenti:

    a. Selezionare **Nome allegato**.

    b. Selezionare **Contenuto allegato**.
    
    c. In hello **è HTML** , quindi selezionare **Sì**.

    ![Finestra di configurazione della posta elettronica di Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Passaggio 7: Salvare e testare il flusso
- In hello **nome flusso** casella, aggiungere un nome per il flusso e quindi fare clic su **creare flusso**.

    ![Finestra di creazione del flusso](./media/app-insights-automate-with-flow/flow8.png)

È possibile attendere hello trigger toorun questa azione, o è possibile eseguire immediatamente dal flusso hello [trigger hello in esecuzione su richiesta](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Quando viene eseguito il flusso di hello, i destinatari hello che è stato specificato nell'elenco di posta elettronica hello visualizzato un messaggio di posta elettronica simile hello seguente:

![Esempio di messaggio di posta elettronica](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sulla creazione di [query di Analisi](app-insights-analytics-using.md).
- Altre informazioni su [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





