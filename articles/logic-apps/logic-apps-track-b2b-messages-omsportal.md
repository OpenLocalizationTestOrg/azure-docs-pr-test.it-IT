---
title: messaggi B2B aaaTrack in Operations Management Suite - App Azure per la logica | Documenti Microsoft
description: Tenere traccia delle comunicazioni B2B per l'account di integrazione e le app per la logica in Operations Management Suite (OMS) con Azure Log Analytics
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Tenere traccia di comunicazione B2B in hello Microsoft Operations Management Suite (OMS)

Dopo avere configurato la comunicazione B2B tra due processi o applicazioni aziendali in esecuzione usando l'account di integrazione, tali entità possono scambiarsi messaggi. toocheck se tali messaggi vengono elaborati correttamente, è possibile tenere traccia di AS2, X12 ed EDIFACT i messaggi con [Azure Log Analitica](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). È ad esempio possibile usare queste funzionalità di rilevamento basate sul Web per tenere traccia dei messaggi:

* Conteggio e stato dei messaggi
* Stato degli acknowledgment
* Correlare i messaggi con i riconoscimenti
* Descrizione dettagliata degli errori
* Funzionalità di ricerca

## <a name="requirements"></a>Requisiti

* Un'app per la logica configurata con la registrazione diagnostica. Informazioni su [come toocreate un'app di logica](logic-apps-create-a-logic-app.md) e [come tooset il livello di registrazione per l'app logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Un account di integrazione configurato con il monitoraggio e la registrazione. Informazioni su [come un account di integrazione toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [come tooset di monitoraggio e registrazione per l'account](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se hai già fatto, [pubblicare dati di diagnostica tooLog Analitica](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) in OMS.

> [!NOTE]
> Dopo che siano soddisfatti i requisiti precedenti hello, è necessario disporre di un'area di lavoro hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). È consigliabile utilizzare hello stessa area di lavoro OMS per la gestione delle comunicazioni B2B in OMS. 
>  
> Se non si dispone di un'area di lavoro OMS, informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Aggiungere la logica App B2B hello soluzione toohello Operations Management Suite (OMS)

toohave OMS tenere traccia dei messaggi B2B per l'app logica, è necessario aggiungere hello **logica App B2B** portale di OMS toohello soluzione. Altre informazioni, vedere [aggiunta di soluzioni tooOMS](../log-analytics/log-analytics-get-started.md).

1. In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**. Cercare "Log Analytics" e quindi scegliere **Log Analytics**, come illustrato qui:

   ![Trovare Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. In **Log Analytics** trovare e selezionare l'area di lavoro di OMS. 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. In **Gestione** scegliere **Portale di OMS**.

   ![Scegliere Portale di OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Al termine, verrà visualizzata la home page di hello OMS, scegliere **Solutions Gallery**.    

   ![Scegliere Raccolta soluzioni](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. In **Tutte le soluzioni** trovare e scegliere **App per la logica B2B**.     

   ![Scegliere App per la logica B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. In **App per la logica B2B** scegliere **Aggiungi**.

   ![Scegliere Aggiungi](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Nella home page di hello OMS, hello riquadro per **logica App B2B messaggi** viene visualizzato. 
   Questo riquadro consente di aggiornare il numero di messaggi hello quando vengono elaborati i messaggi B2B.

   ![Home page di OMS, riquadro Messaggi per le app per la logica B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Lo stato del messaggio di traccia e i dettagli in hello Operations Management Suite

1. Dopo l'elaborazione dei messaggi B2B, è possibile visualizzare lo stato di hello e dettagli dei messaggi. Nella home page di hello OMS, scegliere hello **logica App B2B messaggi** riquadro.

   ![Numero di messaggi aggiornato](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Per impostazione predefinita, hello **logica App B2B messaggi** riquadro vengono visualizzati i dati in base a un solo giorno. ambito dei dati di hello toochange tooa intervallo diverso, scegliere il controllo dell'ambito hello nella parte superiore di hello della pagina OMS hello:
   > 
   > ![Modificare l'ambito dei dati](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Dopo lo stato del messaggio hello viene visualizzato il dashboard, è possibile visualizzare ulteriori dettagli per un tipo di messaggio specifico, che mostra i dati in base a un solo giorno. Scegliere il riquadro hello per **AS2**, **X12**, o **EDIFACT**.

   ![Visualizzare lo stato dei messaggi](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Un elenco di messaggi viene visualizzato per il riquadro scelto. 
   toolearn più sulle proprietà di hello per ogni tipo di messaggio, vedere le descrizioni delle proprietà del messaggio:

   * [Proprietà dei messaggi AS2](#as2-message-properties)
   * [Proprietà dei messaggi X12](#x12-message-properties)
   * [Proprietà dei messaggi EDIFACT](#EDIFACT-message-properties)

   Ecco, ad esempio, come può risultare un elenco di messaggi AS2:

   ![Visualizzare i messaggi AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. input di hello tooview o l'esportazione e output per i messaggi specifici, selezionare i messaggi e scegliere **scaricare**. Quando richiesto, salvare computer locale tooyour di hello file con estensione zip e quindi estrarre il file. 

   la cartella decompressa Hello include una cartella per ogni messaggio selezionato. 
   Se si configurano gli acknowledgement, cartella messaggi hello include anche i file con i dettagli di riconoscimento. 
   Ogni cartella di messaggio include almeno questi file: 
   
   * File leggibile con hello input dettagli payload payload e output
   * File codificati con hello input e output

   Per ogni tipo di messaggio, è possibile trovare la cartella hello e qui i formati del nome file:

   * [Formati dei nomi di file e cartelle AS2](#as2-folder-file-names)
   * [Formati dei nomi di file e cartelle X12](#x12-folder-file-names)
   * [Formati dei nomi di file e cartelle EDIFACT](#edifact-folder-file-names)

   ![Scaricare i file dei messaggi](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview tutte le azioni che hanno hello stesso ID, eseguire su hello **ricerca nei Log** pagina, scegliere un messaggio dall'elenco di messaggi hello.

   È possibile ordinare queste azioni per colonna o cercare risultati specifici.

   ![Azioni con hello stesso ID di esecuzione](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * risultati toosearch con query predefinite, scegliere **Preferiti**.

   * Informazioni su [come toobuild query aggiungendo filtri](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   O altre informazioni, vedere [modalità di ricerca di dati toofind con log nel Log Analitica](../log-analytics/log-analytics-log-searches.md).

   * query toochange nella casella di ricerca hello, aggiornamento hello query con hello colonne e valori che si vuole toouse come filtri.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Descrizioni delle proprietà e formati di nome per i messaggi AS2, X12 ed EDIFACT

Per ogni tipo di messaggio, ecco le descrizioni di proprietà hello e i formati del nome per i file di messaggio scaricato.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Descrizioni delle proprietà dei messaggi AS2

Di seguito sono riportate le descrizioni di proprietà di hello per ciascun messaggio AS2.

| Proprietà | Descrizione |
| --- | --- |
| Mittente | partner guest Hello specificato in **impostazioni di ricezione**, o partner host hello specificato nel **impostazioni di invio** per un accordo AS2 |
| Ricevitore | partner host Hello specificato in **impostazioni di ricezione**, o al partner guest hello specificato in **impostazioni di invio** per un accordo AS2 |
| App per la logica | Hello app per la logica in cui vengono impostate azioni hello AS2 |
| Stato | Hello stato messaggio AS2 <br>Operazione completata = ricevuto o inviato un messaggio AS2 valido. Non sono configurate notifiche sulla ricezione del messaggio. <br>Operazione completata = ricevuto o inviato un messaggio AS2 valido. La notifica sulla ricezione del messaggio è stata configurata e ricevuta o è stata inviata. <br>Operazione non riuscita = ricevuto un messaggio AS2 non valido. Non sono configurate notifiche sulla ricezione del messaggio. <br>In sospeso = ricevuto o inviato un messaggio AS2 valido. La notifica sulla ricezione del messaggio è stata configurata ed è prevista. |
| Ack | stato del messaggio MDN Hello <br>Accettato = ricevuto o inviato un messaggio di notifica sulla ricezione del messaggio positivo. <br>Pending = in attesa tooreceive o inviare un messaggio MDN. <br>Rifiutato = ricevuto o inviato un messaggio di notifica sulla ricezione del messaggio negativo. <br>Non è necessario = MDN non viene impostato nel contratto hello. |
| Direzione | Hello direzione del messaggio AS2 |
| ID correlazione | ID Hello che mette in correlazione tutti i trigger di hello e azioni in un'app di logica |
| ID del messaggio | ID del messaggio Hello AS2 dalle intestazioni del messaggio hello AS2 |
| Timestamp | ora di Hello hello AS2 azione elaborazione messaggio hello |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Formati dei nomi AS2 per i file di messaggi scaricati

Di seguito sono i formati del nome per ogni cartella di messaggi AS2 scaricato e i file hello.

| File o cartella | Formato del nome |
| :------------- | :---------- |
| Cartella del messaggio | [mittente]\_[destinatario]\_AS2\_[ID-correlazione]\_[ID-messaggio]\_[timestamp] |
| File di input, output e, se configurati, acknowledgement | **Payload di input**: [mittente]\_[destinatario]\_AS2\_[ID-correlazione]\_input_payload.txt </p>**Payload di output**: [mittente]\_[destinatario]\_AS2\_[ID-correlazione]\_output\_payload.txt </p></p>**Input**: [mittente]\_[destinatario]\_AS2\_[ID-correlazione]\_inputs.txt </p></p>**Output**: [mittente]\_[destinatario]\_AS2\_[ID-correlazione]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Descrizioni delle proprietà dei messaggi X12

Di seguito sono riportate le descrizioni di proprietà di hello per ogni X12 messaggio.

| Proprietà | Descrizione |
| --- | --- |
| Mittente | partner guest Hello specificato in **impostazioni di ricezione**, o partner host hello specificato nel **impostazioni di invio** per X12 contratto |
| Ricevitore | partner host Hello specificato in **impostazioni di ricezione**, o partner guest hello specificato in **impostazioni di invio** per X12 contratto |
| App per la logica | Hello app per la logica in cui vengono impostate azioni hello X12 |
| Stato | stato del messaggio Hello X12 <br>Operazione completata = ricevuto o inviato un messaggio X12 valido. Non sono configurati ack funzionali. <br>Operazione completata = ricevuto o inviato un messaggio X12 valido. L'ack funzionale è stato configurato e ricevuto o inviato. <br>Operazione non riuscita = ricevuto o inviato un messaggio X12 non valido. <br>In sospeso = ricevuto o inviato un messaggio X12 valido. L'ack funzionale è stato configurato ed è previsto. |
| Ack | Stato ACK funzionale (997) <br>Accettato = ricevuto o inviato un ack funzionale positivo. <br>Rifiutato = ricevuto o inviato un ack funzionale negativo. <br>In sospeso = in attesa di un ack funzionale non ricevuto. <br>In sospeso = generato un ack funzionale, ma non è possibile inviare toopartner. <br>Non richiesto = ack funzionale non configurato. |
| Direzione | direzione del messaggio Hello X12 |
| ID correlazione | ID Hello che mette in correlazione tutti i trigger di hello e azioni in un'app di logica |
| Tipo di messaggio | tipo di messaggio 12 X EDI Hello |
| ICN | Hello numero di controllo interscambio per il messaggio hello X12 |
| TSCN | Hello numero di controllo Set transazioni per il messaggio hello X12 |
| Timestamp | ora di Hello azione hello X12 elaborazione messaggio hello |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>Formati dei nomi X12 per i file di messaggi scaricati

Di seguito sono i formati del nome hello per ogni scaricati X12 cartella e i file dei messaggi.

| File o cartella | Formato del nome |
| :------------- | :---------- |
| Cartella del messaggio | [mittente]\_[destinatario]\_X12\_[numero-controllo-interscambio]\_[numero-controllo-globale]\_[numero-controllo-set-transazioni]\_[timestamp] |
| File di input, output e, se configurati, acknowledgement | **Payload di input**: [mittente]\_[destinatario]\_X12\_[numero-controllo-interscambio]\_input_payload.txt </p>**Payload di output**: [mittente]\_[destinatario]\_X12\_[numero-controllo-interscambio]\_output\_payload.txt </p></p>**Input**: [mittente]\_[destinatario]\_X12\_[numero-controllo-interscambio]\_inputs.txt </p></p>**Output**: [mittente]\_[destinatario]\_X12\_[numero-controllo-interscambio]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Descrizioni delle proprietà dei messaggi EDIFACT

Di seguito sono riportate le descrizioni di proprietà di hello per ogni messaggio EDIFACT.

| Proprietà | Descrizione |
| --- | --- |
| Mittente | partner guest Hello specificato in **impostazioni di ricezione**, o partner host hello specificato nel **impostazioni di invio** per un accordo EDIFACT |
| Ricevitore | partner host Hello specificato in **impostazioni di ricezione**, o al partner guest hello specificato in **impostazioni di invio** per un accordo EDIFACT |
| App per la logica | Hello app per la logica in cui vengono impostate azioni EDIFACT hello |
| Stato | stato del messaggio EDIFACT Hello <br>Operazione completata = ricevuto o inviato un messaggio EDIFACT valido. Non sono configurati ack funzionali. <br>Operazione completata = ricevuto o inviato un messaggio EDIFACT valido. L'ack funzionale è stato configurato e ricevuto o inviato. <br>Operazione non riuscita = ricevuto o inviato un messaggio EDIFACT non valido <br>In sospeso = ricevuto o inviato un messaggio EDIFACT valido. L'ack funzionale è stato configurato ed è previsto. |
| Ack | Stato ACK funzionale (997) <br>Accettato = ricevuto o inviato un ack funzionale positivo. <br>Rifiutato = ricevuto o inviato un ack funzionale negativo. <br>In sospeso = in attesa di un ack funzionale non ricevuto. <br>In sospeso = generato un ack funzionale, ma non è possibile inviare toopartner. <br>Non richiesto = ack funzionale non configurato. |
| Direzione | direzione del messaggio EDIFACT Hello |
| ID correlazione | ID Hello che mette in correlazione tutti i trigger di hello e azioni in un'app di logica |
| Tipo di messaggio | tipo di messaggio EDIFACT Hello |
| ICN | Hello numero di controllo interscambio per il messaggio EDIFACT hello |
| TSCN | Hello numero di controllo Set transazioni per messaggio EDIFACT hello |
| Timestamp | ora di Hello elaborazione messaggio hello hello azione EDIFACT |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Formati dei nomi EDIFACT per i file di messaggi scaricati

Di seguito sono i formati del nome per ogni cartella di messaggi EDIFACT scaricato e i file hello.

| File o cartella | Formato del nome |
| :------------- | :---------- |
| Cartella del messaggio | [mittente]\_[destinatario]\_EDIFACT\_[numero-controllo-interscambio]\_[numero-controllo-globale]\_[numero-controllo-set-transazioni]\_[timestamp] |
| File di input, output e, se configurati, acknowledgement | **Payload di input**: [mittente]\_[destinatario]\_EDIFACT\_[numero-controllo-interscambio]\_input_payload.txt </p>**Payload di output**: [mittente]\_[destinatario]\_EDIFACT\_[numero-controllo-interscambio]\_output\_payload.txt </p></p>**Input**: [mittente]\_[destinatario]\_EDIFACT\_[numero-controllo-interscambio]\_inputs.txt </p></p>**Output**: [mittente]\_[destinatario]\_EDIFACT\_[numero-controllo-interscambio]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Passaggi successivi

* [Cercare i messaggi B2B in Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Schemi di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schemi di rilevamento X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schemi di rilevamento personalizzati](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)