---
title: aaaConnect tooDynamics 365 (online) da Azure logica App | Documenti Microsoft
description: "Creare la logica di flussi di lavoro app per la gestione di entità (online) di Dynamics 365 tramite API fornita da connettore hello Dynamics 365 hello"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Connettersi tooDynamics 365 da flussi di lavoro logica app

Con la logica App, è possibile connettersi tooDynamics 365 (online) e creare flussi di business utile creano record, aggiornare gli elementi o restituiscono un elenco di record. Con il connettore di Dynamics 365 hello, è possibile:

* Compilare il flusso di business in base ai dati hello che si ottiene da Dynamics 365 (online).
* Usare le azioni che ottengono una risposta e l'output di hello rendono disponibili per le altre azioni. Ad esempio, quando viene aggiornato un elemento in Dynamics 365 (online), è possibile inviare un messaggio di posta elettronica con Office 365.

Questo argomento viene illustrato come toocreate un'app di logica che crea un'attività in Dynamics 365 ogni volta che un nuovo cliente potenziale viene creato in Dynamics 365.

## <a name="prerequisites"></a>Prerequisiti
* Un account Azure.
* Un account Dynamics 365 (online).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Creare un'attività quando viene creato un nuovo lead in Dynamics 365

1.  [Accedi tooAzure](https://portal.azure.com).

2.  Nella casella di ricerca di Azure hello, digitare `Logic apps`, e premere INVIO.

      ![Trovare App per la logica](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  In **App per la logica** fare clic su **Aggiungi**.

      ![Aggiungere un'app per la logica](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  app per la logica hello toocreate, hello completo **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso** campi e quindi fare clic su  **Creare**.

5.  Selezionare hello nuova logica app. Quando si riceve hello **distribuzione ha avuto esito positivo** notifica, fare clic su **aggiornamento**.

6.  In **Strumenti di sviluppo** fare clic su **Progettazione app per la logica**. Nell'elenco di modelli di hello, fare clic su **App vuota per la logica**.

7.  Nella casella di ricerca hello, digitare `Dynamics 365`. Da hello Dynamics 365 attiva l'elenco, selezionare **Dynamics 365: quando viene creato un record**.

8.  Nel caso di richiesta toosign in tooDynamics 365, farlo ora.

9.  Nei dettagli trigger hello, immettere hello le seguenti informazioni:

  * **Nome organizzazione**. Selezionare l'istanza di Dynamics 365 di hello che si desidera hello logica app toolisten per.

  * **Nome entità**. Selezionare entità hello che si desidera toolisten per. Questo evento viene utilizzato come un'app di logica di trigger toostart hello. 
  In questa procedura guidata si seleziona **Lead**.

  * **La frequenza desiderata toocheck per gli elementi?** Impostare la frequenza di questi valori hello logica app verifica la presenza di trigger toohello correlati gli aggiornamenti. impostazione predefinita Hello è toocheck per gli aggiornamenti ogni tre minuti.

    * **Frequenza**. Selezionare secondi, minuti, ore o giorni.

    * **Intervallo**. Immettere il numero di hello di secondi, minuti, ore o giorni che si desidera toopass prima hello della successiva archiviazione.

      ![Dettagli del trigger dell'app per la logica](./media/connectors-create-api-crmonline/trigger-details.png)

10. Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.

11. Nella casella di ricerca hello, digitare `Dynamics 365`. Selezionare nell'elenco di azioni hello **Dynamics 365: creare un nuovo record**.

12. Immettere hello le seguenti informazioni:

    * **Nome organizzazione**. Selezionare l'istanza di Dynamics 365 hello in cui si desidera registrazione hello toocreate di hello del flusso. 
    Si noti che questa istanza non dispone di toobe hello stesso in cui hello evento dall'istanza.

    * **Nome entità**. Selezionare entità hello che si desidera toocreate un record quando viene attivato l'evento hello. 
    In questa procedura guidata si seleziona **Attività**.

13. Fare clic nella hello **soggetto** visualizzata. Hello dinamica contenuto elenco visualizzato, è possibile selezionare uno di questi campi:

    * **Cognome**. Selezione di questo campo inserisce hello cognome hello lead campo Subject hello per le attività di hello, quando viene creato il record di attività hello.
    * **Argomento**. Selezionando questa inserimenti hello argomento campo lead hello nel campo soggetto hello per attività di hello, quando i record di attività hello viene creato. 
    Fare clic su **argomento** tooadd che toohello **soggetto** casella.

      ![Dettagli per la creazione di un nuovo record nell'app per la logica](./media/connectors-create-api-crmonline/create-record-details.png)

14. Sulla barra degli strumenti Progettazione applicazione logica hello, fare clic su **salvare**.

    ![Salva nella barra degli strumenti di Progettazione app per la logica](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. hello toostart logica App, fare clic su **eseguire**.

    ![Salva nella barra degli strumenti di Progettazione app per la logica](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Creare ora un record lead in Dynamics 365 for Sales e verificare il funzionamento del flusso.

## <a name="set-advanced-options-for-a-logic-app-step"></a>Impostare le opzioni avanzate per un passaggio dell'app per la logica

toospecify come toofilter dati in un passaggio di app di logica, fare clic su **Visualizza le opzioni avanzate** in questo passaggio, quindi aggiungere un filtro o un ordine dalla query.

Ad esempio, è possibile utilizzare un filtro query tooget solo gli account attivi e ordinare per nome account hello. tooperform questa attività, immettere una query di filtro OData hello `statuscode eq 1`e selezionare **nome Account** dall'elenco di contenuto dinamico hello. Per altre informazioni, vedere [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) e [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Opzioni avanzate delle app per la logica](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Procedure consigliate per l'uso delle opzioni avanzate

Quando si aggiunge un campo del valore tooa, è necessario rispettare il tipo di campo hello digitare un valore o selezionare un valore dall'elenco di contenuto dinamico hello.

Tipo di campo  |Come toouse  |Dove toofind  |Nome  |Tipo di dati  
---------|---------|---------|---------|---------
Campi di testo|I campi di testo richiedono una singola riga di testo oppure contenuto dinamico costituito da un campo di tipo testo. Esempi includono i campi categoria e sottocategoria hello.|Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi |category |Riga di testo singola        
Campi di tipo Integer | Alcuni campi richiedono Integer oppure contenuto dinamico costituito da un campo di tipo Integer. Ad esempio, Percentuale completamento e Durata. |Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi |percentcomplete |Numero intero         
Campi di data | Alcuni campi richiedono una data immessa nel formato mm/gg/aaaa oppure contenuto dinamico costituito da un campo di tipo data. Ad esempio, Data creazione, Data di inizio, Inizio effettivo, Ultimo periodo sospensione, Fine effettiva e Scadenza. | Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi |createdon |Data e ora
Campi che richiedono sia ID record che tipo di ricerca |Alcuni campi che fanno riferimento a un altro record di entità richiedono l'ID record hello e il tipo di ricerca di hello. |Impostazioni > personalizzazioni > Personalizza hello sistema > entità > Account > campi  | accountid  | Chiave primaria

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Alcuni esempi di campi che richiedono sia ID record che tipo di ricerca
Nella tabella precedente hello l'espansione, ecco alcuni esempi di campi che non funzionano con i valori selezionati dall'elenco di contenuto dinamico hello. Al contrario, questi campi richiedono entrambi una ricerca e l'ID tipo di record immesso nei campi hello in PowerApps.  
* Proprietario e Tipo di proprietario. campo proprietario Hello deve essere un ID di record utente o del team valido deve essere il tipo di proprietario Hello **systemusers** o **Team**.
* Cliente e Tipo di cliente. campo Customer Hello deve essere un account valido o record ID contatto. deve essere il tipo di proprietario Hello **account** o **contatti**.
* Tema e Tipo relativo. Hello relativi campi deve essere un ID record valido, ad esempio un account o record ID contatto. Hello per quanto riguarda tipo deve essere il tipo di ricerca hello per record hello, ad esempio **account** o **contatti**.

Hello seguente esempio di azione di creazione di attività aggiunge un account corrispondente di ID di record toohello aggiungerlo toohello riguardanti campo dell'attività hello.

![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid-type-account.png)

In questo esempio viene inoltre assegnato hello attività tooa utente specifico in base a ID del record. dell'utente hello

![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind un record dell'ID, vedere hello seguente sezione: *trovare l'ID record hello*

## <a name="find-hello-record-id"></a>Trovare l'ID record hello

1. Aprire un record, ad esempio un record account.

2. Sulla barra degli strumenti Azioni hello, fare clic su **Pop Out** ![record popout](./media/connectors-create-api-crmonline/popout-record.png).
In alternativa, sulla barra degli strumenti Azioni hello, toocopy hello l'URL completo nel programma di posta elettronica predefinito, fare clic su **posta elettronica un collegamento**.

   ID record Hello viene visualizzato tra hello % 7b e 7 di % d la codifica dei caratteri dell'URL hello.

   ![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi
un passaggio non riuscito in un'app di logica, lo stato hello di visualizzare i dettagli dell'evento hello tootroubleshoot.

1. In **App per la logica**, selezionare l'app per la logica e quindi fare clic su **Panoramica**. 

   Hello area di riepilogo viene visualizzato e fornisce lo stato di esecuzione hello per hello logica app. 

   ![Stato di esecuzione dell'app per la logica](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview ulteriori informazioni su qualsiasi esecuzioni non riuscite, fare clic su hello Impossibile evento. tooexpand un passaggio non riuscito, fare clic su tale passaggio.

   ![Espandere un passaggio non riuscito](./media/connectors-create-api-crmonline/tshoot2.png)

   Dettagli Hello vengono visualizzati e consentono di risolvere problemi che causano hello dell'errore hello.

   ![Dettagli del passaggio non riuscito](./media/connectors-create-api-crmonline/tshoot3.png)

Per altre informazioni sulla risoluzione dei problemi delle app per la logica, vedere [Diagnosi degli errori delle app per la logica](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/crm/). 

## <a name="next-steps"></a>Passaggi successivi
Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).
