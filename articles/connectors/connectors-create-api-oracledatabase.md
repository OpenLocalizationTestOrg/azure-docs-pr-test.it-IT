---
title: connettore di Database Oracle aaaAdd hello nelle app di logica di Azure | Documenti Microsoft
description: Utilizzare il connettore di Oracle Database hello in un'app di logica
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Iniziare con il connettore hello Database Oracle

Con connettore del Database Oracle hello è creare flussi di lavoro aziendali che utilizzano i dati nel database esistente. Questo connettore può connettersi tooan Database Oracle locale o una macchina virtuale Azure con Database Oracle installato. Con questo connettore è possibile:

* Compilare il flusso di lavoro aggiungendo un nuovo database di clienti tooa cliente o l'aggiornamento di un ordine in un database orders.
* Utilizzare azioni tooget una riga di dati, inserire una nuova riga e di eliminare. Quando ad esempio viene creato un record in Dynamics CRM Online (trigger), è possibile inserire una riga in Oracle Database (azione). 

Questo argomento viene illustrato come toouse hello connettore del Database Oracle in un'app di logica.

## <a name="prerequisites"></a>Prerequisiti

* Versioni di Oracle supportate: 
    * Oracle 9 e versioni successive
    * Software client Oracle 8.1.7 e versioni successive

* Installare il gateway dati locale di hello. [Connessione dati tooon locale da App per la logica](../logic-apps/logic-apps-gateway-connection.md) elenchi hello passaggi. gateway Hello è obbligatorio tooconnect tooan Database Oracle locale o una macchina virtuale di Azure con i database Oracle installato. 

    > [!NOTE]
    > gateway dati locale di Hello funge da ponte e fornisce un trasferimento tramite la protezione dei dati tra App per la logica e di dati in locale (dati che non sono nel cloud hello). Hello stesso gateway può essere utilizzato con più servizi e più origini dati. In tal caso, potrebbe essere gateway hello tooinstall una sola volta.

* Installare hello del Client Oracle nel computer di hello in cui è installato gateway dati locale di hello. Assicurarsi di tooinstall hello Provider di dati Oracle a 64 bit per .NET da Oracle:  

  [ODAC 64 bit 12c versione 4 (12.1.0.2.4) per Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Se non è installato il client di Oracle hello, si verifica un errore quando si tenta di toocreate o utilizzare connessione hello. Vedere gli errori comuni di hello in questo argomento.


## <a name="add-hello-connector"></a>Aggiungere il connettore hello

> [!IMPORTANT]
> Questo connettore non include trigger. Ha solo azioni. Pertanto quando si crea la logica app, aggiungere un altro trigger toostart app logica, ad esempio **pianificazione - ricorrenza**, o **richiesta / risposta - risposta**. 

1. In hello [portale di Azure](https://portal.azure.com), creare un'app logica vuoto.

2. All'avvio di hello dell'app logica, selezionare hello **richiesta / risposta - richiesta** trigger: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Selezionare **Salva**. Quando si salva, viene generato automaticamente un URL di richiesta. 

4. Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**. Digitare `oracle` toosee hello azioni disponibili: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > È anche toosee modo più rapido hello hello trigger e le azioni disponibili per i connettori. Digitare parte del nome del connettore hello, ad esempio `oracle`. progettazione di Hello Elenca tutti i trigger e le azioni. 

5. Selezionare una delle operazioni di hello, ad esempio **Database Oracle - Get riga**. Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale). Immettere un nome del server Oracle hello, metodo di autenticazione, username, password e il gateway hello selezionare:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Una volta connesso, selezionare una tabella dall'elenco hello e immettere hello riga ID tooyour tabella. Tooknow hello identificatore toohello tabella è necessaria. Se non si conosce, contattare l'amministratore di database Oracle e ottenere l'output hello `select * from yourTableName`. In questo modo si hello informazioni personali necessarie tooproceed.

    Nell'esempio seguente di hello, dati del processo viene restituiti da un database delle risorse umane: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. In questo passaggio successivo, è possibile utilizzare uno qualsiasi dei hello toobuild altri connettori il flusso di lavoro. Se si desidera tootest recupero dei dati da Oracle, invia un messaggio di posta elettronica con i dati di Oracle hello utilizzando uno dei hello inviare posta elettronica connettori, tali Office 365 o Gmail. Usare i token dinamico hello da hello toobuild tabella Oracle di hello `Subject` e `Body` del messaggio di posta elettronica:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Salvare** l'app per la logica e quindi selezionare **Esegui**. Chiudere Progettazione hello ed esaminare hello cronologia di esecuzione per lo stato di hello. In caso contrario, selezionare una riga messaggio hello. verrà visualizzata la finestra di progettazione Hello e mostra che passaggio non è riuscita e mostra inoltre hello informazioni sull'errore. Se ha esito positivo, verrà visualizzato un messaggio di posta elettronica con le informazioni di hello che è stato aggiunto.


### <a name="workflow-ideas"></a>Idee per i flussi di lavoro

* Si desidera toomonitor hello #oracle hashtag e inserire TWEET hello in un database in modo che possono essere eseguite query e utilizzate all'interno di altre applicazioni. In un'app di logica, aggiungere hello `Twitter - When a new tweet is posted` attivare, quindi immettere hello **#oracle** hashtag. Aggiungere quindi hello `Oracle Database - Insert row` azione, quindi selezionare la tabella:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* I messaggi vengono inviati tooa della coda del Bus di servizio. Si desidera tooget questi messaggi e inserirli in un database. In un'app di logica, aggiungere hello `Service Bus - when a message is received in a queue` trigger e coda hello selezionare. Aggiungere quindi hello `Oracle Database - Insert row` azione, quindi selezionare la tabella:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Errori comuni

#### <a name="error-cannot-reach-hello-gateway"></a>**Errore**: Impossibile raggiungere hello Gateway

**Causa**: gateway dati locale di hello non è in grado di tooconnect toohello cloud. 

**Attenuazione**: verificare che il gateway è in esecuzione nel computer locale di hello in cui è stato installato e che può connettersi toohello internet.  Si consiglia di non installare il gateway hello in un computer che può essere disattivata o sospensione. È anche possibile riavviare il servizio hello locale data gateway (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Errore**: hello provider in uso è deprecato: ' OracleClient richiede software client Oracle versione 8.1.7 o versione successiva.'. Visitare [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall provider ufficiale di hello.

**Causa**: hello Oracle client SDK non è installato nel computer di hello dove hello locali gateway dati è in esecuzione.  

**Risoluzione**: scaricare e installare il client Oracle hello SDK in hello stesso computer del gateway dati locale di hello.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Errore**: La tabella '[NomeTabella]' non definisce alcuna colonna chiave

**Causa**: tabella hello non dispone di qualsiasi chiave primaria.  

**Risoluzione**: connettore del Database Oracle hello è necessario utilizzare una tabella con una colonna chiave primaria.

#### <a name="currently-not-supported"></a>Attualmente non supportati

* Viste e stored procedure 
* Tabelle con chiavi composte
* Tipi di oggetti annidati nelle tabelle
 
## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/oracle/). 

## <a name="get-some-help"></a>Ottenere aiuto

Hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) è inserire domande tooask, rispondere alle domande e osservare gli altri utenti di App per la logica sono un'eccellente. 

È possibile migliorare App per la logica e i connettori votando e inviando le idee nella pagina [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Passaggi successivi
[Creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md)ed esplorare i connettori disponibili hello in App per la logica nel nostro [elenco API](apis-list.md).
