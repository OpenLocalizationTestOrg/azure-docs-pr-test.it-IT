---
title: aaaAutomate Azure Application Insights elabora tramite App per la logica.
description: "Informazioni su come è possibile automatizzare rapidamente processi ripetibili aggiungendo hello Application Insights connettore tooyour logica app."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Automatizzare i processi di Application Insights con app per la logica

È possibile trovare autonomamente ripetutamente in hello stesse query il toocheck di dati di telemetria se il servizio funziona correttamente? Tooautomate esaminando queste query per individuare tendenze e anomalie e quindi compilare i propri flussi di lavoro attorno a esse? il connettore di Azure Application Insights Hello (anteprima) per App per la logica è strumento appropriato hello a questo scopo.

Con questa integrazione è possibile automatizzare numerosi processi senza dover scrivere una sola riga di codice. È possibile creare un'app logica con Application Insights hello tooquickly connettore automatizzare qualsiasi processo di Application Insights. 

È possibile aggiungere anche altre azioni. funzionalità di App per la logica di Hello di servizio App di Azure rende disponibili centinaia di azioni. Usando un'app per la logica, è ad esempio possibile inviare automaticamente una notifica di posta elettronica o creare un bug in Visual Studio Team Services. È inoltre possibile utilizzare uno dei hello disponibili molti [modelli](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp velocizzare il processo di hello di creazione dell'applicazione di logica. 

## <a name="create-a-logic-app-for-application-insights"></a>Creare un app per la logica per Application Insights

In questa esercitazione viene illustrato come toocreate attributi di un'applicazione di logica che utilizza hello Analitica autocluster algoritmo toogroup nei dati di hello per un'applicazione web. flusso Hello invia automaticamente i risultati di hello tramite posta elettronica, solo un esempio di come è possibile utilizzare Application Insights Analitica e la logica App contemporaneamente. 

### <a name="step-1-create-a-logic-app"></a>Passaggio 1: Creare un'app per la logica
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. In hello **New** riquadro, selezionare **Web e dispositivi mobili**, quindi selezionare **logica App**.

    ![Finestra della nuova app per la logica](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Passaggio 2: Creare un trigger per l'app per la logica
1. In hello **progettazione applicazione logica** finestra, in **iniziare con un trigger**selezionare **ricorrenza**.

    ![Finestra di progettazione di app per la logica](./media/automate-with-logic-apps/logicapp2.png)

2. In hello **frequenza** , quindi selezionare **giorno** e quindi nel hello **intervallo** digitare **1**.

    !["Ricorrenza" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Passaggio 3: Aggiungere un'azione di Application Insights
1. Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.

2. In hello **scegliere un'azione** nella casella di ricerca **Azure Application Insights**.

3. Fare clic su **Application Insights - Visualize Analytics query Preview** (Application Insights - Visualizza query di Analisi Anteprima) in **Azioni**.

    !["Scegliere un'azione" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Passaggio 4: Connettere la risorsa di Application Insights tooan

toocomplete questo passaggio, è necessario un ID applicazione e una chiave API per la risorsa. È possibile recuperarli dal portale di Azure hello, come illustrato nel seguente diagramma hello:

![ID dell'applicazione nel portale di Azure hello](./media/automate-with-logic-apps/appid.png) 

Specificare un nome per la connessione, un ID applicazione hello e una chiave API hello.

![Connessione per il flusso nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Passaggio 5: Specificare hello query Analitica e tipo di grafico
Nell'esempio seguente di hello, query hello Seleziona richieste hello non riuscito all'interno di hello ultimo giorno e li correla le eccezioni che si è verificato come parte dell'operazione di hello. Analitica correla le richieste di hello non è riuscita, in base all'identificatore hello operation_Id. query Hello segmenti quindi risultati hello utilizzando l'algoritmo autocluster hello. 

Quando si crea la propria query, verificare che funzionino correttamente in Analitica prima di aggiungerlo tooyour flusso.

1. In hello **Query** aggiungere hello query Analitica seguenti: 

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

2. In hello **tipo di grafico** , quindi selezionare **tabella Html**.

    ![Finestra di configurazione della query di Analisi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Passaggio 6: Configurare la posta elettronica toosend di hello logica app

1. Fare clic su **Nuovo passaggio** e selezionare **Aggiungi un'azione**.

2. Nella casella di ricerca hello, digitare **Outlook di Office 365**.

3. Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).

    ![Selezione di Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. In hello **invia un messaggio di posta elettronica** finestra hello seguenti:

   a. Digitare l'indirizzo di posta elettronica hello del destinatario hello.

   b. Digitare un oggetto per la posta elettronica hello.

   c. Fare clic nella hello **corpo** casella e quindi su hello contenuto menu dinamico che consente di aprire hello destro, selezionare **corpo**.

   d. Fare clic su **Mostra opzioni avanzate**.

      ![Configurazione di Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. Nel menu del contenuto dinamico hello hello seguenti:

    a. Selezionare **Nome allegato**.

    b. Selezionare **Contenuto allegato**.
    
    c. In hello **è HTML** , quindi selezionare **Sì**.

      ![Schermata di configurazione della posta elettronica di Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Passaggio 7: Salvare e testare l'app per la logica
* Fare clic su **salvare** toosave le modifiche.

È possibile attendere hello trigger toorun hello logica app oppure è possibile eseguire immediatamente hello logica app selezionando **eseguire**.

![Schermata di creazione dell'app per la logica](./media/automate-with-logic-apps/step7.png)

Quando viene eseguita l'app logica, i destinatari di hello specificato nell'elenco di posta elettronica hello riceveranno un messaggio di posta elettronica simile hello seguente:

![Messaggio di posta elettronica dell'app per la logica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sulla creazione di [query di Analisi](app-insights-analytics-using.md).
- Altre informazioni su [App per la logica](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





