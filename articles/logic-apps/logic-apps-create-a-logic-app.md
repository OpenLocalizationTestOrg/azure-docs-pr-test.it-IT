---
title: aaaCreate il primo flusso di lavoro tra le app cloud e servizi cloud - App Azure per la logica | Documenti Microsoft
description: Automatizzare i processi aziendali per scenari di integrazione di sistemi e di Enterprise Application Integration (EAI) creando ed eseguendo flussi di lavoro in App per la logica di Azure
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: flusso di lavoro, app cloud, servizi cloud, processi aziendali, integrazione di sistemi, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Creare la prima app logica processi tooautomate di flusso di lavoro tra le app cloud e servizi cloud

Senza scrivere codice, è possibile automatizzare i processi aziendali in modo più semplice e rapido durante la creazione ed esecuzione di flussi di lavoro con [App per la logica di Azure](logic-apps-what-are-logic-apps.md). Il primo esempio mostra come toocreate un flusso di lavoro app logica di base che controlla un RSS feed per il nuovo contenuto in un sito Web. Quando nuovi elementi vengono visualizzati nel feed del sito Web di hello, hello logica app Invia messaggio di posta elettronica da un account di Outlook o Gmail.

toocreate ed eseguire un'app di logica, è necessario questi elementi:

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/). In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).

  La sottoscrizione di Azure viene usata per la fatturazione dell'utilizzo delle app per la logica. Per altre informazioni, vedere le pagine relative alla [misurazione dell'utilizzo](../logic-apps/logic-apps-pricing.md) e ai [prezzi](https://azure.microsoft.com/pricing/details/logic-apps) per App per la logica di Azure.

Questo esempio richiede anche gli elementi seguenti:

* Account Outlook.com, Office 365 Outlook o Gmail

    > [!TIP]
    > Se si ha un [account Microsoft](https://account.microsoft.com/account) personale, si ha un account Outlook.com. Se invece si una un account Azure aziendale o dell'istituto di istruzione, si ha un account **Office 365 Outlook**.

* Un collegamento di tooa feed RSS del sito Web. Questo esempio viene utilizzato hello [feed RSS per ultimissime dal sito Web CNN.com hello](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Aggiungere un trigger che avvia il flusso di lavoro

Oggetto [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che inizia il flusso di lavoro logica app ed è primo elemento hello necessari all'app di logica.

1. Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").

2. Scegliere dal menu a sinistra hello **New** > **Enterprise Integration** > **logica App** come illustrato di seguito:

     ![Portale di Azure, Nuovo, Enterprise Integration, App per la logica](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > È anche possibile scegliere **New**, digitare nella casella di ricerca hello `logic app`, e premere INVIO. Scegliere quindi **App per la logica** > **Crea**.

3. Assegnare un nome all'app per la logica e selezionare la sottoscrizione di Azure. Creare quindi o selezionare un gruppo di risorse di Azure, che consente di organizzare e gestire le risorse di Azure correlate. Infine, selezionare l'ubicazione del Data Center hello per le app per la logica di hosting. Quando si è pronti, scegliere **Pin toodashboard** e quindi **crea**.

     ![Dettagli dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Quando si seleziona **toodashboard Pin**, app logica viene visualizzata nel dashboard di Azure hello dopo la distribuzione e viene aperta automaticamente. Se l'app logica non viene visualizzato nel dashboard hello hello **tutte le risorse** riquadro, scegliere **vedere più**e selezionare l'app logica. O scegliere dal menu a sinistra, hello **più servizi**. In **Enterprise Integration** scegliere **App per la logica**, quindi selezionare l'app per la logica.

4. Quando si apre l'app per la logica per hello prima volta, hello progettazione applicazione logica mostra i modelli che è possibile usare tooget avviato. Per il momento, scegliere **App per la logica vuota**, per consentire la creazione di un'app per la logica completamente nuova.

    Apre Hello progettazione applicazione logica e vengono mostrati i servizi disponibili e *trigger* che è possibile utilizzare nell'applicazione logica.

5. Nella casella di ricerca hello, digitare `RSS`e selezionare il trigger: **RSS - quando viene pubblicato un elemento del feed** 

    ![Trigger di RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Immettere il collegamento hello per feed RSS del sito Web di hello che si desidera tootrack. 

     È anche possibile cambiare i valori per **Frequenza** e **Intervallo**. 
     Queste impostazioni determinano la frequenza con cui l'app per la logica verifica la presenza di nuovi elementi e restituisce tutti gli elementi trovati durante tale periodo di tempo.

     Per questo esempio, controlliamo ogni giorno per le storie superiore registrato del sito Web CNN toohello.

     ![Configurare un trigger con feed RSS, frequenza e intervallo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Salvare il lavoro, per il momento. (Nella barra dei comandi della finestra di progettazione hello, scegliere **salvare**.)

   ![Salvare l'app per la logica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Quando si salva, logica app passa in tempo reale, ma attualmente la logica app controlla solo per i nuovi elementi nel feed RSS hello. 
   toomake in questo esempio più utile, che si aggiunge un'azione che esegue l'app per la logica del trigger after viene attivato.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Aggiunge un'azione che risponde tooyour trigger

Un'[*azione*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica. Dopo avere aggiunto un'app di logica tooyour trigger, è possibile aggiungere un tooperform operazioni con i dati generati dal trigger. Per questo esempio, è ora possibile aggiungere un'azione che invia messaggio di posta elettronica quando vengono visualizzati nuovi elementi nel feed RSS del sito Web di hello.

1. Nella finestra di progettazione hello in trigger, scegliere **nuovo passaggio** > **aggiungere un'azione** come illustrato di seguito:

   ![Aggiungere un'azione](media/logic-apps-create-a-logic-app/add-new-action.png)

   finestra di progettazione Mostra Hello [connettori disponibili](../connectors/apis-list.md) in modo che è possibile selezionare tooperform un'azione quando il trigger viene attivato.

2. Basato su account di posta elettronica, seguire i passaggi di hello per Outlook o Gmail.

   * messaggio di posta elettronica toosend dall'account Outlook, nella casella di ricerca hello, immettere `outlook`. In **Servizi** scegliere **Outlook.com** per gli account Microsoft personali oppure **Office 365 Outlook** per gli account Azure aziendali o dell'istituto di istruzione. 
   In **Azioni** selezionare **Invia un messaggio di posta elettronica**.

       ![Selezionare l'azione "Invia un messaggio di posta elettronica" di Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * messaggio di posta elettronica toosend dall'account Gmail, nella casella di ricerca hello, immettere `gmail`. 
   In **Azioni** selezionare **Invia messaggio di posta elettronica**.

       ![Scegliere "Gmail - Invia messaggio di posta elettronica"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Quando viene chiesto di immettere le credenziali, accedere con hello username e password per l'account di posta elettronica. 

4. Fornire dettagli di hello per questa azione, come indirizzo di posta elettronica di destinazione hello e scegliere parametri hello per hello dati tooinclude nel messaggio di posta elettronica di hello, ad esempio:

   ![Selezionare dati tooinclude nel messaggio di posta elettronica](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Se è stato scelto Outlook, l'app per la logica potrebbe avere un aspetto simile a questo esempio:

    ![App per la logica completata](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Salvare le modifiche. (Nella barra dei comandi della finestra di progettazione hello, scegliere **salvare**.)

6. È ora possibile eseguire manualmente l'app per la logica per i test. Nella barra dei comandi della finestra di progettazione hello, scegliere **eseguire**. In caso contrario, è possibile consentire l'app logica verificare hello specificato feed RSS basato su pianificazione hello impostati.

   Se l'app logica consente di individuare nuovi elementi, hello logica app Invia messaggio di posta elettronica che include i dati selezionati. 
   Se non è stato trovato alcun nuovo elemento, l'app logica Ignora azione hello che invia messaggio di posta elettronica.

7. toomonitor e controllare le app per la logica di esecuzione del e attivare cronologia, nel menu logica app, scegliere **Panoramica**.

   ![Monitorare e visualizzare la cronologia di esecuzione e dei trigger dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Se non si trova dati hello previsti, sulla barra dei comandi di hello, provare a scegliere **aggiornamento**.

   ulteriori informazioni sullo stato dell'applicazione logica toolearn o eseguire e attivare cronologia o toodiagnose app logica, vedere [app logica di risoluzione dei problemi](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > L'esecuzione dell'app per la logica continua fino alla disattivazione dell'app. tooturn disattivare l'app per il momento, nel menu logica app, scegliere **Panoramica**. Nella barra dei comandi di hello, scegliere **disabilitare**.

La prima app per la logica è stata configurata ed eseguita. È stato anche illustrato come creare con facilità flussi di lavoro per l'automazione dei processi e integrare le app cloud e i servizi cloud, senza scrivere codice.

## <a name="manage-your-logic-app"></a>Gestire l'app per la logica

toomanage l'app, è possibile eseguire attività come controllare lo stato di hello, modificare, visualizzare la cronologia, disattivare o eliminare l'app logica.

1. Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").

2. Scegliere dal menu a sinistra, hello **più servizi**. In **Enterprise Integration** scegliere **App per la logica**. Selezionare l'app per la logica. 

   Nel menu di applicazione hello logica, è possibile trovare queste attività di gestione di app logica:

   |Attività|Passi| 
   |:---|:---| 
   | Visualizzare lo stato, la cronologia di esecuzione e le informazioni generali dell'app| Scegliere **Panoramica**.| 
   | Modificare l'app | Scegliere **Progettazione app per la logica**. | 
   | Visualizzare la definizione JSON del flusso di lavoro dell'app | Scegliere **Visualizzazione codice app per la logica**. | 
   | Visualizzare le operazioni eseguite nell'app per la logica | Scegliere **Log attività**. | 
   | Visualizzare le versioni precedenti per l'app per la logica | Scegliere **Versioni**. | 
   | Disattivare temporaneamente l'app | Scegliere **Panoramica**, quindi nella barra dei comandi di hello, scegliere **disabilitare**. | 
   | Eliminare l'app | Scegliere **Panoramica**, quindi nella barra dei comandi di hello, scegliere **eliminare**. Immettere il nome dell'app per la logica e scegliere **Elimina**. | 

## <a name="get-help"></a>Ottenere aiuto

rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

*  [Aggiungere condizioni ed eseguire flussi di lavoro](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Modelli di app per la logica](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Creare app per la logica da modelli di Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md)
