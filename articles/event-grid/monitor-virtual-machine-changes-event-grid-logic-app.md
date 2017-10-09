---
title: modifiche di macchina virtuale aaaMonitor - app di logica e griglia di eventi di Azure | Documenti Microsoft
description: Controllare le modifiche di configurazione apportate a macchine virtuali usando Griglia di eventi di Azure e app per la logica
keywords: app per la logica, griglie di eventi, macchina virtuale, VM
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Monitorare le modifiche a una macchina virtuale con Griglia di eventi di Azure e app per la logica

È possibile avviare un [flusso di lavoro di app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) automatizzato quando si verificano determinati eventi in risorse di Azure o in risorse di terze parti. Queste risorse è possono pubblicare tali tooan eventi [griglia eventi Azure](../event-grid/overview.md). A sua volta, griglia di eventi hello inserisce tali toosubscribers eventi con code e ai webhook, o [hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md) come endpoint. Come sottoscrittore, l'app logica può attendere per gli eventi dalla griglia di eventi di hello prima dell'esecuzione di flussi di lavoro automatizzati attività tooperform - senza che sia necessario scrivere codice.

Ad esempio, ecco alcuni eventi che i server di pubblicazione può inviare toosubscribers tramite il servizio di griglia di eventi di Azure hello:

* Creare, leggere, aggiornare o eliminare una risorsa. È possibile, ad esempio, monitorare le modifiche che possono generare addebiti sulla sottoscrizione di Azure e influire quindi sui costi. 
* Aggiungere o rimuovere un utente da una sottoscrizione di Azure.
* L'app esegue una determinata azione.
* In una coda viene visualizzato un nuovo messaggio.

Questa esercitazione consente di creare un'app di logica che esegue il monitoraggio di macchina virtuale tooa di modifiche e invia messaggi di posta elettronica su tali modifiche. Quando si crea un'app logica con una sottoscrizione di eventi per una risorsa di Azure, flusso di eventi da tale risorsa tramite un'app per la logica toohello griglia evento. Hello esercitazione viene illustrata la creazione di questa app logica:

![Panoramica - Monitorare una macchina virtuale con Griglia di eventi e un'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un'app per la logica che consenta di monitorare gli eventi da Griglia di eventi.
> * Aggiungere una condizione che controlli in modo specifico le modifiche apportate a una macchina virtuale.
> * Inviare un messaggio di posta elettronica quando viene apportata una modifica alla macchina virtuale.

## <a name="prerequisites"></a>Prerequisiti

* Un account di posta elettronica di [un provider di posta elettronica supportato da App per la logica di Azure](../connectors/apis-list.md), come Office 365 Outlook, Outlook.com o Gmail, per l'invio di notifiche. In questa esercitazione viene usato Office 365 Outlook.

* Una [macchina virtuale](https://azure.microsoft.com/services/virtual-machines). Se questa operazione non è già stata eseguita, creare una macchina virtuale mediante l'[esercitazione Creare una macchina virtuale](https://docs.microsoft.com/azure/virtual-machines/). macchina virtuale di hello toomake pubblicare eventi, si [non necessario toodo qualsiasi altra operazione](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Creare un'app per la logica che consenta di monitorare gli eventi da Griglia di eventi

Innanzitutto, creare un'app di logica e aggiungere un trigger di evento della griglia che consente di monitorare hello gruppo di risorse per la macchina virtuale. 

1. Accedi toohello [portale di Azure](https://portal.azure.com). 

2. Hello angolo superiore sinistro del menu Azure principale hello, scegliere **New** > **Enterprise Integration** > **logica App**.

   ![Creare l'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Creare app logica con impostazioni hello specificate in hello nella tabella seguente:

   ![Specificare i dettagli dell'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Impostazione | Valore consigliato | Descrizione | 
   | ------- | --------------- | ----------- | 
   | **Nome** | *{nome-app-per-logica}* | Specificare un nome univoco per l'app per la logica. | 
   | **Sottoscrizione** | *{sottoscrizione-Azure-personale}* | Selezionare hello stessa sottoscrizione di Azure per tutti i servizi in questa esercitazione. | 
   | **Gruppo di risorse** | *{gruppo-risorse-Azure-personale}* | Selezionare hello stesso gruppo di risorse di Azure per tutti i servizi in questa esercitazione. | 
   | **Posizione** | *{area-Azure-personale}* | Selezionare hello stessa area per tutti i servizi in questa esercitazione. | 
   | | | 

4. Quando si è pronti, selezionare **Pin toodashboard**e scegliere **crea**.

   È stata creata ora una risorsa di Azure per l'app per la logica. 
   Dopo che Azure distribuisce l'app logica, hello logica App Designer viene modelli per i modelli comuni in modo da poter iniziare più rapidamente.

   > [!NOTE] 
   > Quando si seleziona **toodashboard Pin**, app logica viene aperto automaticamente nella finestra di progettazione logica app. In caso contrario, è possibile trovare e aprire manualmente l'app per la logica.

5. Scegliere ora un modello di app per la logica. In **Modelli** scegliere **App per la logica vuota** per creare un'app per la logica completamente nuova.

   ![Selezionare il modello dell'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   ora Mostra Hello logica App progettazione [ *connettori* ](../connectors/apis-list.md) e [ *trigger* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) che è possibile utilizzare toostart la logica app, nonché azioni che è possibile aggiungere dopo un'attività tooperform trigger. Un trigger è un evento che crea un'istanza dell'app per la logica e avvia il flusso di lavoro dell'app per la logica. 
   L'app logica deve un trigger come primo elemento hello.

6. Nella casella di ricerca hello, immettere "griglia di eventi" come filtro. Selezionare questo trigger: **Azure Event Grid - On a resource event** (Griglia di eventi di Azure - Per un evento della risorsa)

   ![Selezionare questo trigger: Azure Event Grid - On a resource event (Griglia di eventi di Azure - Per un evento della risorsa)](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Quando richiesto, accedere tooAzure griglia eventi con le credenziali di Azure.

   ![Accedere con le credenziali di Azure](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Se hai effettuato l'accesso con un account Microsoft personale, ad esempio @outlook.com o @hotmail.com, i trigger di evento griglia hello potrebbe non essere visualizzati correttamente. In alternativa, scegliere [Connetti con entità servizio](/azure-resource-manager/resource-group-create-service-principal-portal.md), o eseguire l'autenticazione come un membro di hello Azure Active Directory associato alla sottoscrizione Azure, ad esempio, *nome utente* @emailoutlook.onmicrosoft.com.

8. La sottoscrizione a questo punto gli eventi di toopublisher logica app. Fornire dettagli di hello per la sottoscrizione dell'evento come specificato in hello nella tabella seguente:

   ![Specificare i dettagli della sottoscrizione eventi](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Impostazione | Valore consigliato | Descrizione | 
   | ------- | --------------- | ----------- | 
   | **Sottoscrizione** | *{sottoscrizione-Azure-macchina-virtuale}* | Selezionare la sottoscrizione Azure del server di pubblicazione hello evento. Per questa esercitazione, selezionare hello sottoscrizione di Azure per la macchina virtuale. | 
   | **Tipo di risorsa** | Microsoft.Resources.resourceGroups | Selezionare il tipo di risorsa del server di pubblicazione hello evento. Per questa esercitazione, selezionare hello valore specificato in modo app logica consente di monitorare solo i gruppi di risorse. | 
   | **Nome risorsa** | *{nome-gruppo-risorse-macchina-virtuale}* | Selezionare il nome di risorsa del server di pubblicazione di hello. Per questa esercitazione, selezionare il nome di hello hello del gruppo di risorse per la macchina virtuale. | 
   | Per visualizzare le impostazioni facoltative, scegliere **Mostra opzioni avanzate**. | *{Vedere descrizioni}* | * **Prefix Filter** (Filtro prefisso): per questa esercitazione, lasciare vuota questa impostazione. comportamento predefinito di Hello corrisponde a tutti i valori. È possibile tuttavia specificare una stringa di prefisso come filtro, ad esempio un percorso o un parametro relativo a una determinata risorsa. <p>* **Suffix Filter** (Filtro suffisso): per questa esercitazione, lasciare vuota questa impostazione. comportamento predefinito di Hello corrisponde a tutti i valori. È possibile tuttavia specificare una stringa di suffisso come filtro, ad esempio un'estensione se si vuole usare solo specifici tipi di file.<p>* **Nome sottoscrizione**: specificare un nome univoco per la sottoscrizione eventi. |
   | | | 

   Al termine di questa operazione, il trigger di Griglia di eventi dovrebbe avere un aspetto simile all'esempio seguente:
   
   ![Dettagli del trigger di Griglia di eventi di esempio](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Salvare l'app per la logica. Sulla barra degli strumenti della finestra di progettazione hello scegliere **salvare**. toocollapse e nascondere i dettagli di un'azione nell'app logica, scegliere barra del titolo dell'azione hello.

   ![Salvare l'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Quando si salva la logica app con un trigger di evento della griglia, Azure crea automaticamente una sottoscrizione di eventi per la risorsa di logica app tooyour selezionato. Quando la risorsa hello pubblica una griglia di eventi eventi toohello, pertanto tale griglia di eventi inserisce automaticamente hello evento tooyour logica app. Questo evento attiva app logica, quindi crea ed esegue un'istanza del flusso di lavoro hello definita nella procedura successiva.

Logica app è ora in tempo reale e in ascolto tooevents dalla griglia di eventi hello, ma non esegue alcuna operazione fino a quando non si aggiunge del flusso di lavoro toohello azioni. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Aggiungere una condizione che controlli le modifiche apportate a una macchina virtuale

toorun logica dell'applicazione flusso di lavoro solo quando si verifica un evento specifico, aggiungere una condizione che controlla per la macchina virtuale "operazioni di scrittura". Quando questa condizione è true, l'app logica invia di posta elettronica con i dettagli sulla macchina virtuale hello aggiornato.

1. In Progettazione App logica nel trigger di hello evento griglia, scegliere **nuovo passaggio** > **aggiungere una condizione**.

   ![Aggiungi condizione tooyour logica app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Hello logica App Designer consente di aggiungere una condizione vuoto tooyour del flusso di lavoro, inclusi azione percorsi toofollow basata se hello condizione è true o false.

   ![Condizione vuota](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. In hello **condizione** scegliere **modifica nella modalità avanzata**.
Immettere questa espressione:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   La condizione dovrebbe avere ora un aspetto simile all'esempio seguente:

   ![Condizione vuota](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Questa espressione Controlla eventi di hello `body` per un `data` oggetto dove hello `operationName` proprietà è hello `Microsoft.Compute/virtualMachines/write` operazione. 
   Per altre informazioni, vedere [Schema di eventi di Griglia di eventi](../event-grid/event-schema.md).

3. una descrizione per la condizione di hello, tooprovide scegliere hello **puntini di sospensione** (**...** ) sulla barra forma condizione hello, quindi scegliere **rinominare**.

   > [!NOTE] 
   > Hello esempi più avanti in questa esercitazione anche forniscono le descrizioni per i passaggi del flusso di lavoro di hello logica app.

4. Ora scegliere **modificare in modalità base** in modo che l'espressione hello risolve automaticamente come illustrato:

   ![Condizione dell'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Salvare l'app per la logica.

## <a name="send-email-when-your-virtual-machine-changes"></a>Inviare un messaggio di posta elettronica quando viene apportata una modifica alla macchina virtuale

A questo punto aggiungere un [ *azione* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) in modo che sia possibile ottenere un messaggio di posta elettronica quando hello specificato condizione è true.

1. In condizione di hello **se ha valore true** scegliere **aggiungere un'azione**.

   ![Aggiungere un'azione se la condizione viene soddisfatta](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. Nella casella di ricerca hello, immettere "email" come filtro. In base ai provider di posta elettronica, è possibile individuare e selezionare connettore corrispondente hello. Selezionare quindi l'azione "Invia il messaggio di posta elettronica" hello per il connettore. ad esempio: 

   * Per un Azure di lavoro o scuola account, il connettore di Outlook di Office 365 selezionare hello. 
   * Per gli account Microsoft personali, selezionare il connettore di Outlook.com hello. 
   * Per gli account Gmail, selezionare il connettore di Gmail hello. 

   Verrà toocontinue con connettore di Office 365 Outlook hello. 
   Se si utilizza un provider diverso, hello passi rimangono hello stesso, ma l'interfaccia utente potrebbe avere diverso. 

   ![Selezionare l'azione di invio di un messaggio di posta elettronica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Se si dispone già una connessione per il provider di posta elettronica, accedi tooyour account di posta elettronica quando viene richiesto per l'autenticazione.

4. Fornire dettagli per la posta elettronica hello come specificato in hello nella tabella seguente:

   ![Azione di posta elettronica vuota](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect dai campi disponibili nel flusso di lavoro, fare clic in una casella di modifica in modo che hello **contenuto dinamico** viene aperto l'elenco oppure scegliere **aggiungere contenuto dinamico**. Per ulteriori campi, scegliere **più** per ogni sezione nell'elenco di hello. hello tooclose **contenuto dinamico** scegliere **aggiungere contenuto dinamico**.

   | Impostazione | Valore consigliato | Descrizione | 
   | ------- | --------------- | ----------- | 
   | **To** | *{indirizzo-postaelettronica-destinatario}* |Immettere l'indirizzo di posta elettronica del destinatario hello. AI fini del test delle app è possibile indicare il proprio indirizzo di posta elettronica. | 
   | **Oggetto** | Risorse aggiornate: **Oggetto**| Immettere il contenuto di hello per l'oggetto del messaggio hello. Per questa esercitazione, immettere hello suggerito di testo e dell'evento hello selezionare **soggetto** campo. In questo caso, l'oggetto messaggio di posta elettronica include il nome di hello per la risorsa aggiornata hello (macchina virtuale). | 
   | **Corpo** | Gruppo di risorse: **Argomento** <p>Tipo di evento: **Tipo di evento**<p>ID evento: **ID**<p>Ora: **Ora evento** | Immettere il contenuto di hello per il corpo del messaggio hello. Per questa esercitazione, immettere hello suggerito di testo e dell'evento hello selezionare **argomento**, **tipo di evento**, **ID**, e **ora evento** campi in modo che messaggio di posta elettronica include nome gruppo di risorse hello, tipo di evento, il timestamp degli eventi e ID di evento per l'aggiornamento di hello. <p>tooadd righe vuote nel contenuto, premere MAIUSC + INVIO. | 
   | | | 

   > [!NOTE] 
   > Se si seleziona un campo che rappresenta una matrice, finestra di progettazione hello aggiunge automaticamente un **per ogni** cerchio attorno azione hello che fa riferimento la matrice hello. In questo modo, l'app per la logica esegue l'azione su ogni elemento della matrice.

   L'azione di invio di un messaggio di posta elettronica avrà ora un aspetto simile all'esempio seguente:

   ![Selezionare gli output tooinclude tramite posta elettronica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   Al termine di questa operazione, l'app per la logica dovrebbe avere un aspetto simile all'esempio seguente:

   ![App per la logica completata](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Salvare l'app per la logica. toocollapse e nascondere i dettagli di ogni azione nell'app logica, scegliere barra del titolo dell'azione hello.

   ![Salvare l'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   L'app di logica è ora in tempo reale, ma è in attesa per la macchina virtuale tooyour modifiche prima di eseguire alcuna operazione. 
   tootest logica app, continuare toohello nella sezione successiva.

## <a name="test-your-logic-app-workflow"></a>Testare il flusso di lavoro per l'app per la logica

1. gli eventi specificati che stanno hello app logica toocheck, aggiornare la macchina virtuale. 

   Ad esempio, è possibile ridimensionare la macchina virtuale nel portale di Azure hello o [ridimensionare la macchina virtuale con Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Dopo alcuni istanti, si dovrebbe ricevere un messaggio di posta elettronica. ad esempio:

   ![Messaggio di posta elettronica sull'aggiornamento della macchina virtuale](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. viene eseguito tooreview hello e della cronologia di trigger per l'app di logica, nel menu logica app, scegliere **Panoramica**. tooview ulteriori dettagli sull'esecuzione, scegliere la riga hello per quell'esecuzione.

   ![Cronologia di esecuzioni di app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. tooview hello input e output per ogni passaggio, espandere il passaggio di hello che si desidera tooreview. Queste informazioni consentono di eseguire la diagnostica e il debug di problemi nell'app per la logica.
 
   ![Dettagli della cronologia di esecuzioni dell'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Congratulazioni, è stata creata ed eseguita un'app per la logica in grado di monitore gli eventi di risorse tramite Griglia di eventi e di inviare un messaggio di posta elettronica quando si verificano tali eventi. Si è inoltre appreso come creare con facilità flussi di lavoro per l'automazione dei processi e come integrare sistemi e servizi cloud.

## <a name="clean-up-resources"></a>Pulire le risorse

In questa esercitazione vengono usate risorse ed eseguite azioni che generano addebiti sulla sottoscrizione di Azure. Pertanto una volta terminato con l'esercitazione hello e il test, assicurarsi di disabilitare o eliminare tutte le risorse in cui si desidera tooincur addebiti.

È possibile arrestare l'applicazione di logica di esecuzione e l'invio di posta elettronica senza eliminare l'applicazione hello. Scegliere **Panoramica** dal menu dell'app per la logica. Sulla barra degli strumenti hello, scegliere **disabilitare**.

![Disabilitare l'app per la logica](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>domande frequenti

**D**: Quali altre attività di monitoraggio delle macchine virtuali è possibile eseguire con Griglia di eventi e le app per la logica? </br>
**R**: È possibile monitorare altre modifiche di configurazione, ad esempio:

* L'acquisizione da parte di una macchina virtuale dei diritti di controllo degli accessi in base al ruolo.
* Tooa rete gruppo di sicurezza () su un'interfaccia di rete (NIC) vengono apportate modifiche.
* L'aggiunta o la rimozione di dischi in una macchina virtuale.
* Un indirizzo IP pubblico assegnato scheda NIC del tooa macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica di Griglia di eventi](../event-grid/overview.md)
* [Concetti relativi a Griglia di eventi](../event-grid/concepts.md)
* [Guida introduttiva: Creare e instradare eventi personalizzati con la griglia di eventi](../event-grid/custom-event-quickstart.md)
* [Schema di eventi di Griglia di eventi](../event-grid/event-schema.md)
* [App per la logica di Azure](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Creare flussi di lavoro di app per la logica con modelli predefiniti](../logic-apps/logic-apps-use-logic-app-templates.md)